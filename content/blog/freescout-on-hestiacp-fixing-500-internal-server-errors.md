---
title: 'FreeScout on HestiaCP: Fixing 500 Internal Server Errors'
slug: freescout-on-hestiacp-fixing-500-internal-server-errors
date: 2026-07-07T00:24:00+05:30
image: ''
author:
  - Ronak Vanpariya
categories:
  - Technology
  - Solutions
tags:
  - Hestia CP
  - FreeScout
  - Self-Hosting
  - Laravel
  - Sysadmin
description: Learn to install freescout on Hestiacp or Getting a 500 error installing FreeScout on HestiaCP? Learn how to fix open_basedir restrictions, whitelist PHP functions, and clear poisoned queues.
keywords: []
draft: false
---

So, you want to build a "community-first, private-second" support funnel for your plugins or software. You’ve wisely chosen **bbPress** for the public, Google-indexed forum layer, and you want **FreeScout** (the magnificent, self-hosted open-source HelpDesk) to securely handle the private tickets where customers hand over sensitive staging credentials.

You also have **HestiaCP** running your server because you like clean control panels and automated Let's Encrypt SSLs. 

You think to yourself: _"I’ll just upload the zip, click next, and be done in 5 minutes."_

**Cue the dramatic music.** 🎬

Instead of a beautiful dashboard, you are greeted by the developer's favorite jumpscare: **500 Internal Server Error**. 

If you are currently staring at that error, take a deep breath. Here is the ultimate, battle-tested guide to getting FreeScout running cleanly on HestiaCP, written in the blood of real-time debugging logs.

***

## Step 1: The Standard HestiaCP Setup

Before the fireworks begin, let’s do the basic setup correctly.

1. **Create the Database:** In HestiaCP, go to **DB** and add a new database (e.g., `helphub_db`). Save your user and password.
2. **Add the Subdomain:** Go to **Web**, add your subdomain (e.g., `support.example.com`), and check **Enable SSL (Let's Encrypt)**.
3. **The Laravel Special:** Under **Advanced Options**, change your Backend Template (PHP-FPM) to **PHP 8.2**. Then, check **Custom document root** and type `public`. 
   > 💡 _Why? FreeScout is built on Laravel. The internet should only ever see the `public` folder, not your core system configuration files._
4. **Upload the Files:** Download the latest FreeScout release `.zip` from GitHub. Use Hestia’s File Manager to upload it into `public_html`, and extract it right there.

Now you visit your URL... and boom. **500 Error.** Let’s fix it.

***

## Boss Level 1: The `.htaccess` Saboteur

You open your Apache/Nginx error logs and spot this weird line:
`.../public_html/.htaccess: <IfModule not allowed here`

### The Lesson:

FreeScout ships with an `.htaccess` file in its root directory meant for basic shared hosting users who can't change their document root. Because you _already_ changed your document root to `public` inside HestiaCP, this root file is not only useless, it’s actively breaking Apache security policies.

### The Fix:

Go into your HestiaCP File Manager, find the `.htaccess` file sitting directly in `public_html`, and **delete it** (or rename it to `old.htaccess`). 
_(Note: Do NOT touch the `.htaccess` file inside the `public/` folder. That one is required for routing!)_

***

## Boss Level 2: The `open_basedir` Trap

You delete the file, refresh, and get another 500 error:
`PHP Warning: require(): open_basedir restriction in effect.`

### The Lesson:

By telling HestiaCP that your document root is the `public` folder, Hestia’s security policy strictly locks PHP inside that folder. But Laravel needs to look one folder up to read its core `.env` configuration file. 

### The Fix:

You need to lift the `open_basedir` restriction for your PHP template. SSH into your server as `root` and edit the master template:

````bash
nano /usr/local/hestia/data/templates/web/php-fpm/PHP-8_2.tpl



Find the line starting with `php_admin_value[open_basedir]` and comment it out by placing a semicolon at the beginning:

Plaintext

```plain
;php_admin_value[open_basedir] = ...
````

Save (`Ctrl+O`, `Enter`, `Ctrl+X`) and apply the update via terminal (replace `admin` with your Hestia username):

Bash

```plain
v-change-web-domain-backend-tpl admin support.example.com PHP-8_2
```

## Boss Level 3: The Disabled Security Functions

You finally reach the beautiful FreeScout installation wizard! You enter your database info, create your admin user, log in, and click around. Suddenly... more crashes. You check the application logs (`storage/logs/laravel.log`) and see:

`Error: Call to undefined function App\Misc\shell_exec()`

`Call to undefined function Illuminate\Queue\pcntl_alarm()`

### The Lesson:

HestiaCP is paranoid—and rightfully so. It disables powerful PHP functions like `shell_exec` and the `pcntl_*` process controls by default. But FreeScout is a complex background worker; it _needs_ these functions to manage email queues and background processes.

Because FreeScout runs via a web interface **and** a background Cron Job, you must remove these restrictions from **both** the FPM (Web) and CLI (Terminal) configurations.

### The Fix:

Open the FPM configuration:

Bash

```plain
nano /etc/php/8.2/fpm/php.ini
```

And open the CLI configuration:

Bash

```plain
nano /etc/php/8.2/cli/php.ini
```

In both files, press `Ctrl+W`, search for `disable_functions`, and remove `shell_exec`, `pcntl_alarm`, `pcntl_signal`, and `pcntl_async_signals` from the list. Save them, then restart PHP:

Bash

```plain
systemctl restart php8.2-fpm
```

## Boss Level 4: The Poisoned Queue

After enabling the PHP functions, you realize your helpdesk can _send_ emails, but it refuses to _fetch_ new ones. The logs reveal a giant wall of text ending in:

`App\Jobs\RestartQueueWorker has been attempted too many times or run too long. The job may have previously timed out.`

### The Lesson:

While you were busy fixing the PHP functions earlier, the FreeScout background cron job was trying to run over and over again. Because it kept failing, Laravel eventually marked the background job as "poisoned" to keep it from crashing your CPU. Now that the server is healthy, the system is still refusing to run the old, stuck tasks.

### The Fix:

You need to flush the toilet. Navigate to your FreeScout folder and run these artisan commands to reset the cache and clear the stuck queue.

_⚠️ Pro-Tip: Run these commands as your Hestia application user (e.g., `freescout` or `admin`), NOT as root, or you will break your folder permissions!_

Bash

```plain
cd /home/your_user/web/[support.example.com/public_html](https://support.example.com/public_html)

# Flush the broken state
php artisan cache:clear
php artisan queue:flush
php artisan queue:restart
```

## The Victory Lap: Activating the Cron Job

Now that the system is entirely unblocked, clean, and reset, we need to activate the automated heart of FreeScout.

In your HestiaCP dashboard, navigate to the **Cron** tab and click **Add Cron Job**.

Set the schedule to run **every minute** (put an asterisk `*` in the Minute, Hour, Day, Month, and Wday fields), and enter the official execution command:

Bash

```plain
php /home/your_user/web/[support.example.com/public_html/artisan](https://support.example.com/public_html/artisan) schedule:run >> /dev/null 2>&1
```

Click save, look back at your screen, and watch the emails start seamlessly pouring into your new, beautifully self-hosted helpdesk.

### Summary Checklist for a Happy FreeScout

- [x] Document root set to `/public`
- [x] Parent `.htaccess` deleted
- [x] `open_basedir` disabled in the template
- [x] `shell_exec` and `pcntl_` functions whitelisted in FPM & CLI
- [x] Queue flushed after fixing restrictions
- [x] `schedule:run` cron job firing every 60 seconds

Happy hosting! Your community now has a secure, private escape hatch for advanced troubleshooting.
