---
aliases: 
date: 2020-07-15
description: 
published: true
keywords: 
layout: note
title: Saving space in Terraform
tags:
  - devops
  - terraform
---

In [[Terraform]], by default `terraform init` will automatically download the providers/plugins and modules and place them under `.terraform` in the current working directory.
This is very convenient as it treat each "Terraform project" as independent configuration.

At work as a [[DevOps]] engineer I have many AWS resources managed using Terraform and it is awesome. Each part is configured as separate "project" this is very useful when it comes to debugging, also we find it more convenient not having to risk to affect the whole infrastructure while making changes on some part of it. 

On the other hand, running `terraform init` in each of them would download a copy of the AWS provider which is roughly 150Mb, clearly the number adds up pretty fast.

Similar to the `node_modules` case, this may lead to many copy of the same package (or provider, in Terraform's case). While having separate `node_modules` in web-development is actually relevant for dependency management, having ten copies of the same version AWS provider doesn't really seem to be very useful.

According to the documentation (https://www.terraform.io/docs/extend/how-terraform-works.html#plugin-locations)
I can manually install plugins under `$HOME/.terraform.d/plugins` and Terraform would be able to catch it.

In fact, Terraform first checks the locally installed plugins and then searches the required ones from the configuration.

---

Update:

Previously I mentioned about manually installing plugins under `$HOME/.terraform.d/plugins`
The annoyance would be having to manually move the new plugins every time there is an install.

I found out that Terraform has something that helps with this out of the box which is plugin caching (https://www.terraform.io/docs/configuration/providers.html#provider-plugin-cache)

The only thing that I missed is that it creates hard links by default, which on a `ls` (personally, I like [`exa`](https://github.com/ogham/exa) ) does show up like a copy of the file.

The motivation of this has been explained here: https://github.com/hashicorp/terraform/issues/20609
So in the end of the day it still saves space and it feels less hacky!
