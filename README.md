Mediawiki-Model
===============

Model is extension for mediawiki brings "M" from MVC pattern into MediaWiki.

![Model](http://i.imgur.com/kn1bvbB.png)

What is Model?
==============

- [Examples]

Very simple and lightweight thing. See examples:

- Without Model - fetch all users:
  
```php
  $dbr = wfGetDB( DB_SLAVE );
  $users = $dbr->select(
     'user',
      array( 'user_id', 'user_name' ),
      __METHOD__   
  );
  $fetchedUsers = array();
  while ( $user = $users->fetchObject() ) {
    $fetchedUsers[] = $user;
  }
```

- With Model - fetch all users:
  
```php
  $users = Model_User::find();
```

- Without Model - fetch user id for user name:

```php
  $dbr = wfGetDB( DB_SLAVE );
  $result = $dbr->select(
    'user',
    array('*'),
    array('user_name' => 'John'),
    __METHOD__
  );
  $user = $result->fetchObject();
  print $user->user_id;
```
  
- With Model - fetch user id for user name:

```php
  $user = Model_User::find( array( 'user_name' => 'John' ) );
  print $user[0]->user_id;
```

- Without Model - update user name:

```php
  $dbr = wfGetDB( DB_MASTER );
  $dbr->update(
    'users',
    array( 'user_name' => 'NewName' ),
    array( 'user_id' => $user_id ),
    __METHOD__
  );
```

- With Model - update user name:

```php
  $user = Model_User::find( array( 'user_name' => 'John' ) );
  $user[0]->user_name = 'NewName';
  $user->save();
```

- With Model - create new user:

```php
  $user = new Model_User();
  $user->user_name = 'John Name';
  $insertId = $user->save();
```

- With Model - delete user:

```php
  $user = Model_User::find( array( 'user_name' => 'John' ) );
  $user[0]->delete();
```

- With Model - create new user on form request:

```php
  //Form 'user create' was posted
  if( $wgRequest->wasPosted() ) {
    $user = new Model_User();
    if( $user->validate() ) {
      $user->save();
    } 
  }
```

- With Model - update existing user on form request:

```php
  //Form 'user create' was posted
  $userId = $wgRequest->getval('userid');
  if( $wgRequest->wasPosted() ) {
    $user = new Model_User( $userId );
    if( $user->validate() ) {
      $user->save();
    }
  }
```

How to use it?
======
