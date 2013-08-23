# JForrst
A jQuery plugin to fetch post and user info from the Forrst API

## Dependencies
For normal usage; jQuery 1.3 or higher.

## Usage
JForrst makes available methods for retrieving shot and player information from the Forrst.com API. All the available methods are accessed from the JForrst object which is a member of the jQuery or $ object.

### Get a Post
$.jforrst.getUserPosts(username, callback)

**Parameters**
* > username string.
* > callback FUNC Function to call once the request has completed successfully. One parameter will be passed containing the JSON response of the request; callback(data).

**Example**
```
$.jforrst.getUserPosts("IvanSotelo", function(data){
                    var html = [];

                $.each(data.resp.posts, function (i, posts) {
                    html.push('<li>');
                    html.push('<div class="details"><h3>' + posts.title + '</h3>');
                    html.push('<h4>by <a href="' + posts.user.url + '">' + posts.user.username + '</a></h4></div>');
                    html.push('<a href="' + posts.post_url + '" target="_blank" class="linkc">');
                    html.push('<img src="' + posts.multiposts[1].snaps.mega_url + '" alt="' + posts.title + '">');
                    html.push('</a></li>');
                });
    
                $('#shotsListing').html(html.join(''));
                }, {page: 1, per_page: 8
                });    
```
