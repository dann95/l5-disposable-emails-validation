# Laravel 5 Disposable E-mails Validation
>This repo uses [ivolo/disposable-email-domains](https://github.com/ivolo/disposable-email-domains) to update the black list.

## How to install?
```bash
composer require dann95/l5-disposable-emails-validation
```
## How to use?
#### Add service provider in config/app.php

```php
    [
        //...
        App\Providers\AppServiceProvider::class,
        App\Providers\AuthServiceProvider::class,
        // App\Providers\BroadcastServiceProvider::class,
        App\Providers\EventServiceProvider::class,
        App\Providers\RouteServiceProvider::class,
        Dann95\L5DisposableEmails\Providers\DisposableEmailsServiceProvider::class /* add it here */
        //...
    ],
```

#### Using inside Http/Requests
```php
    /**
     * Get the validation rules that apply to the request.
     *
     * @return array
     */
    public function rules()
    {
        return [
            'email' => ['required','email','real_email'],
        ];
    }

    /**
     * @return array
     */
    public function messages()
    {
        return [
            'email.real_email' => 'Sorry you are using temporary e-mail',
        ];
    }
```

#### Using inside Http/Controller
```php
public function store(Request $request)
{
    $this->validate($request, [
        'email' => 'required|email|real_email',
    ]);
    // the email is valid
}
```

#### Using anywhere
```php
    $validator = Validator::make(request()->all(), [
        'email' => 'required|email|real_email',
    ]);

    if ($validator->fails()) {
        // it fails
    }
```
