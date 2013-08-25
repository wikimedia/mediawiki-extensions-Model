Mediawiki-Model
===============

Model is extension for mediawiki brings "M" from MVC pattern into MediaWiki.

![Model](http://i.imgur.com/kn1bvbB.png)

What is Model?
==============

Very simple and lightweight thing. See example:
  - Without Model:
  
```php
  $dbr = wfGetDB( DB_SLAVE );
  $users = $dbr->select(
     'user',
       array( 'user_id', 'user_name' )
     );
  $fetchedUsers = array();
  while ( $user = $users->fetchObject() ) {
    $fetchedUsers[] = $user;
  }
```

  - With Model:
  
```php
  $users = Model_User::find();
```

  - Without Model:

```php
  $dbr = wfGetDB( DB_SLAVE );
  $result = $dbr->select(
    'user',
    array('*'),
    array('user_name' => 'John')
  );
  $user = $result->fetchObject();
  print $user->user_id;
```
  
  - With Model:

```php
  $user = Model_User::find( array( 'user_name' ) );
  print $user[0]->user_id;
```

  
