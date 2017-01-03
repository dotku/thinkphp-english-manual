## Infrastructure Overview

ThinkPHP 5.0 application is based on MVC (Model-View-Controller) program design pattern.

The visit of 5.0 URL is designed by router. If the router is turned off or there is no configuration for router,
the URL is base on:

> http://serverName/index.php (or other application's entry file) /Module/Controller/Action/[Parameter Name/Value ...]

(to be continue ...)

## Life Cycle

In this chapter, we will introduce the life cycle of ThinkPHP 5.0 Application for helping developers understand the 
whole execution flow.  

(to be continue ...)

## Entry File

ThinkPHP is using single entry mode to deploy project and visit. For any purpose, one application should have a 
consolidated (but not must be only one) entry point.

In general, all application is start from a entry file, and the entry file for different application should be similar.

(to be continue ...)

## URL Visit

### URL Design

By default, ThinkPHP 5.0 is using classic URL visit rule:

> http://serverName/index.php (or other application's entry file) /Module/Controller/Action/[Parameter Name/Value ...]

(to be continue ...)
## Module Design

5.0 version make module more flexible. It is using multiple module structure by default, and support single module design. 
All module namespace start from app (it is configurable).

(to be continue ...)

## Namespace

ThinkPHP 5 is using namespace to load class library file automatically. It is efficient way to solve the multiple 
module and Composer class library namespace conflict issue, and successfully create high performance autoload 
mechanism.

(to be continue ...)

## Autoload

ThinkPHP 5.0 fully implement request loading. All library is using auto load mechanism, and support library point and 
composer class library auto loading.

(to be continue ...)

## Traits Feature

ThinkPHP 5.0 starts using trial feature (PHP 5.4+) for extend mechanism. It could make one class multiple inherit.

(to be continue ...)

## API Friendly

New ThinkPHP improve API development, and won't relay on the old API extend method.

(to be continue ...)