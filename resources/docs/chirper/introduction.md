# <b>01.</b> Introduction

Selamat Datang di Laravel Bootcamp! In this guide we will walk through building a modern Laravel application from scratch. To explore the framework, we'll build a microblogging platform called _Chirper_.

Laravel is incredibly flexible, allowing you to build your front-end with a wide variety of technologies to suit your needs. For this tutorial, we will use Blade.

### Blade

[Blade](https://laravel.com/docs/blade) is the simple, yet powerful templating engine that is included with Laravel. Your HTML will be rendered server-side, making it a breeze to include dynamic content from your database. We'll also be using [Tailwind CSS](https://tailwindcss.com/) to make it look great!

If you're not sure where to start, we think Blade is the most straight-forward. You can always come back and build Chirper again using JavaScript.

```blade filename=welcome.blade.php
Greetings {{ $friend }}, let's build Chirper with Blade!
```

<a href="/blade/installation" class="relative inline-flex mt-2 no-underline border border-red-600 group focus:outline-none">
    <span class="inline-flex items-center self-stretch justify-center w-full px-4 py-2 text-sm font-bold text-center text-red-600 uppercase transition-transform transform bg-white dark:bg-dark-700 ring-1 ring-red-600 ring-offset-1 dark:ring-offset-dark-600 group-hover:-translate-y-1 group-hover:-translate-x-1 group-focus:-translate-y-1 group-focus:-translate-x-1">Build Chirper with Blade</span>
</a>
