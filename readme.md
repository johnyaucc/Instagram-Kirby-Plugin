# Instagram Plugin for Kirby by Simon Albrecht (1.0)
This is a plugin for [Kirby](http://getkirby.com/) that loads images from the [Instagram](http://instagram.com/) API.

## Installation
1. Put the `instagram.php` file in your `site/plugins` folder. If this folder doesn't exist yet, create it.
2. In order to interact with the Instagram API, you need to obtain an access token for yourself.
3. Visit http://instagr.am/developer/client/register/ and register an application.
4. Copy the Client-ID of the newly created app.
5. Visit `https://instagram.com/oauth/authorize/?client_id=CLIENT-ID&redirect_uri=http://albrecht.me/tools/params.php&response_type=token` in your browser, but replace CLIENT-ID with your client-id. **Note** The callback-url points to a simple ([open source](https://gist.github.com/1738919)) tool I wrote for better display of the params passed to a callback url.
6. Copy the access_token and/or save it somewhere.
7. Implement the plugin into your template.

## Update instructions
To update, just replace the old `instagram.php` file in `site/plugins`, with the new one.

## Example usage
	<?php
    // Load an instagram object using your access_token (see installation)
    // containing 10 shots.
    // Note: Replace XXX… with your access_token
    $instagram  = instagram('XXX.XXXXXXX.XXXXXXXXXXXXXXXXXXXXXXXXX', 10);
    $images	    = $instagram->images();

    foreach ($images as $image): ?>
        <div class="instagram-photo">
            <a href="<?php echo $image->link ?>"><img src="<?php echo $image->url ?>" /></a>
            <div class="location">
                <span><?php echo $image->location ?> (<?php echo $image->latitude ?>, <?php echo $image->longitude ?>)</span>
            </div>
        </div>
	<?php endforeach ?>
	
**Advanced Users:** See the source for further options.

## Attributes for the image
* `$images->link` The link to the image
* `$images->comments` The number of comments
* `$images->likes` The number of likes
* `$images->created` The timestamp when the image was created
* `$images->thumb` The url of the thumbnail of the image
* `$images->url` The url of the full-sized image
* `$images->image_lowres` The url to a low-res version of the image
* `$images->filter` The filter that was used
* `$images->location` The location name
* `$images->latitude` The latitude of the location
* `$images->longitude` The longitude of the image
* `$images->tags` An array of tags of the image

## Attributes for the user-object
* `$user->username` The username of the user
* `$user->full_name` The full name of the user
* `$user->picture` The url to the avatar of the user

## Requirements
Your web server must have support for cURL [(installation instructions)](http://www.php.net/manual/en/curl.installation.php)

## Author
Copyright 2012, Simon Albrecht [http://albrecht.me/](http://albrecht.me).
If you use this plugin, feel free to ping me [@s_albrecht](http://twitter.com/s_albrecht).