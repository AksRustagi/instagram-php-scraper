# Instagram PHP Scrapper
This library based on Instagram web version. We develop it because nowadays it is hard to get approved Instagram application. 
The purpose support every feature that web desktop and mobile version support. 

## Code Example
```php
$instagram = Instagram::withCredentials('username', 'password');
$instagram->login();
$account = $instagram->getAccountById(3);
echo $account->getUsername();
```
Some methods does not require auth: 
```php
$instagram = new Instagram();
$nonPrivateAccountMedias = $instagram->getMedias('kevin');
echo $nonPrivateAccountMedias[0]->getLink();
```
If you use auth it is recommended to cash user session, in this case you don't need run `$instagram->login()` method every time your program runs:

```php
$instagram = Instagram::withCredentials('username', 'password', '/path/to/cache/folder/');
$instagram->login(); // will use cached session if you can force login $instagram->login(true)
$account = $instagram->getAccountById(3);
echo $account->getUsername();
```

## Installation

### Using composer

```sh
composer require raiym/instagram-php-scraper
```

### If you don't have composer
You can download it [here](https://getcomposer.org/download/).

## Examples
See examples [here](https://github.com/postaddictme/instagram-php-scraper/tree/master/examples).



### Some of following examples outdated (fixing it)

if you need to get medias by tags or locations:
```php
$instagram = Instagram::withCredentials('username', 'password');
$instagram->login();
// And then you will be able to query instagram with newly updated methods. (Notice that these methods are not static anymore)

$medias $instagram->getLocationTopMediasById(1)
$medias = $instagram->getLocationMediasById(1);
$medias = $instagram->getTopMediasByTagName('hello');
```

### Search medias by tag name
```php
$medias = Instagram::getMediasByTag('zara', 30);
echo json_encode($medias);
```

### Paginate medias by tag name
```php
$result = Instagram::getPaginateMediasByTag('zara');
$medias = $result['medias']

if($result['hasNextPage'] === true) {
    $result = Instagram::getPaginateMediasByTag('zara', $result['maxId']);
    $medias = array_merge($medias, $result['medias']);
}

echo json_encode($medias);
```

### Get top medias by tag name
```php
$medias = Instagram::getTopMediasByTagName('durov');
```

### Get media by id
```php
$media = Instagram::getMediaById(1270593720437182847)
```

### Convert media id to shortcode
```php
echo 'CODE: ' . Media::getCodeFromId('1270593720437182847_3');
// OR
echo 'CODE: ' . Media::getCodeFromId('1270593720437182847');
// OR
echo 'CODE: ' . Media::getCodeFromId(1270593720437182847);
// CODE: BGiDkHAgBF_
// So you can do like this: instagram.com/p/BGiDkHAgBF_
```

### Convert shortcode to media id
```php
echo 'Media id: ' . Media::getIdFromCode('BGiDkHAgBF_');
// Media id: 1270593720437182847
```

### Get location top medias by location id
```php
$medias = Instagram::getLocationTopMediasById(1);
```

### Get location medias by location id
```php
$medias = Instagram::getLocationMediasById(1);
```

## Other
Java library: https://github.com/postaddictme/instagram-java-scraper