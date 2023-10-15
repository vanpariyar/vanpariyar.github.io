---
title: "PHPCS Setup Useful Commands"
slug: "phpcs-setup-useful-commands"
date: 2023-10-14T23:14:11+05:30
# image : "https://ia800508.us.archive.org/25/items/blog-images_202309/White%20Blue%20Illustration%20Business%20Blog%20Banner.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["PHPCS", "PHP", "WordPress"]
# meta description
description: "In this article I have shared the some commands that help me to setup PHPCS easily"
keywords: ["WordPress and PHP setup with PHPCS and PHPCBF", "Useful commands for the PHPCS", "What is PHPCS and how to use it"]
# save as draft
draft: false  
---

Hello everyone, :wave:

**PHP Setup Useful Commands**

This blog post will discuss a useful PHP setup command that can be used to add the current working directory to the PHPCS installed paths. This can be useful for projects that use custom PHP coding standards or rulesets.

**What is PHPCS?**

PHPCS is a PHP Coding Standards Fixer. It is a tool that can be used to check PHP code for compliance with a variety of coding standards, such as PSR-1, PSR-2, and PEAR. PHPCS can also be used to fix some coding errors automatically.

**What are PHPCS installed paths?**

PHPCS installed paths are the directories that PHPCS will search for coding standards and rulesets. By default, PHPCS will search the following directories:

* The `src/Standards` directory of the PHPCS installation.
* The `Standards` directory of the current working directory.

**How to add the current working directory to the PHPCS installed paths**

To add the current working directory to the PHPCS installed paths, you can use the following command:

```shell
phpcs_ipath=$(phpcs --config-show installed_paths); oldpath=${phpcs_ipath##*:}; phpcs --config-set installed_paths ${oldpath},$(pwd)
```

This command will first get the current PHPCS installed paths using the `phpcs --config-show installed_paths` command. It will then remove the leading colon from the installed paths using the `oldpath=${phpcs_ipath##*:}` command. Finally, it will set the PHPCS installed paths to the old installed paths plus the current working directory using the `phpcs --config-set installed_paths ${oldpath},$(pwd)` command.

Once you have run this command, the current working directory will be added to the PHPCS installed paths. This means that PHPCS will be able to find any custom PHP coding standards or rulesets that are located in the current working directory.

**Example usage**

The following example shows how to use the command to add the current working directory to the PHPCS installed paths:

```shell
# Get the current PHPCS installed paths.
phpcs_ipath=$(phpcs --config-show installed_paths)

# Remove the leading colon from the installed paths.
oldpath=${phpcs_ipath##*:};

# Set the PHPCS installed paths to the old installed paths plus the current working directory.
phpcs --config-set installed_paths ${oldpath},$(pwd)
```

Once you have run this command, the current working directory will be added to the PHPCS installed paths. You can then use PHPCS to check your PHP code for compliance with the custom coding standards or rulesets that are located in the current working directory.

Thanks For Reading 🙏

> This articles is generated Manually from generative AI, But carefully reviewed by Me personally. Please let me know if you found any issues, in comment section below.

{{< footer-donation >}}