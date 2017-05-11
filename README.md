# Laravel 5 Friendships

[![Build Status](https://travis-ci.org/merodiro/Friendships.svg?branch=master)](https://travis-ci.org/merodiro/Friendships) [![Code Climate](https://codeclimate.com/github/merodiro/Friendships/badges/gpa.svg)](https://codeclimate.com/github/merodiro/Friendships) [![Test Coverage](https://codeclimate.com/github/merodiro/Friendships/badges/coverage.svg)](https://codeclimate.com/github/merodiro/Friendships/coverage) [![Total Downloads](https://img.shields.io/packagist/dt/merodiro/Friendships.svg?style=flat)](https://packagist.org/packages/merodiro/Friendships) [![Version](https://img.shields.io/packagist/v/merodiro/Friendships.svg?style=flat)](https://packagist.org/packages/merodiro/Friendships) [![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat)](LICENSE)


This package gives users the ability to manage their friendships.

## Models can:
- Send Friend Requests
- Accept Friend Requests
- Deny Friend Requests
- Delete Friend

## Installation

First, install the package through Composer.

```php
composer require merodiro/friendships
```

Then include the service provider inside `config/app.php`.

```php
'providers' => [
    ...
    Merodiro\Friendships\FriendshipsServiceProvider::class,
    ...
];
```
Publish config and migrations


#### optional
if you want to edit it
```
php artisan vendor:publish --provider="Merodiro\Friendships\FriendshipsServiceProvider"
```

Finally, migrate the database
```
php artisan migrate
```

## Setup a Model
```php
use Merodiro\Friendships\Friendable;
class User extends Model
{
    use Friendable;
    ...
}
```

## How to use
[Check the Test file to see the package in action](https://github.com/merodiro/Friendships/blob/master/tests/FriendshipsTest.php)

#### Send a Friend Request
```php
$user->addFriend($recipient);
```

#### Accept a Friend Request
```php
$user->acceptFriend($sender);
```

#### Deny a Friend Request
```php
$user->delteFriend($sender);
```

#### Remove Friend
```php
$user->delteFriend($friend);
```

#### check the current relation between two users
```php
$user->checkFriendship($anotherUser);
```
it returns

* `friends` => if they are friends
* `waiting` => if the first user sent request to the second
* `pending` => if the second user sent request to the first
* `not friends` => if they are not friends and no friend requests



## Friends
To get a collection of users use the following methods:
#### Get Friends
```php
$user->friends();
```

#### Get a list of users who sent friend request to `$user`
```php
$user->friendRequestsTo();
```

#### Get a list of users who have friend requests from `$user`
```php
$user->friendRequestsFrom();
```

## Events
This is the list of the events fired by default for each action

|Event name            |Fired                            |
|----------------------|---------------------------------|
|friendrequest.sent    |When a friend request is sent    |
|friendrequest.accepted|When a friend request is accepted|
|friendship.deleted    |When a friend request is denied  |
|friendship.deleted    |When a friendship is cancelled   |