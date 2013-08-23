# JForrst
A jQuery plugin to fetch post and user info from the Forrst API

## Dependencies
For normal usage; jQuery 1.3 or higher.

## Usage
JForrst makes available methods for retrieving shot and player information from the Forrst.com API. All the available methods are accessed from the JForrst object which is a member of the jQuery or $ object.

### Get User info
$.jforrst.getUserInfo(username, callback)

**Parameters**
* > username string.
* > callback FUNC Function to call once the request has completed successfully. One parameter will be passed containing the JSON response of the request; callback(data).

**Example**
```
$.jforrst.getUserInfo("IvanSotelo", function(data){
    var html = [];

    html.push('<a href="' + data.resp.url + '"><img src="' +  data.resp.photos.large_url + '" alt=""></a>');
    html.push('<div><h3>' + data.resp.name + '</h3>');
    html.push('<h4><a href="' + data.resp.url + '">' + data.resp.url + '</a></h4>');
    html.push('<ul><li><b>Posts: </b>' + data.resp.posts + '</li>');
    html.push('<li><b>Following: </b>' +  data.resp.following + '</li>');
    html.push('<li><b>Followers: </b>' +  data.resp.followers + '</li>');
    html.push('<li><b>Likes: </b>' +  data.resp.likes + '</li></ul></div>');

    $('#userInfo').html(html.join(''));
                });    
```

### Get a Posts
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

### Get a Post
$.jforrst.getPostsShow(postId, callback)

**Parameters**
* > postId INT The id of the post.
* > callback FUNC Function to call once the request has completed successfully. One parameter will be passed containing the JSON response of the request; callback(data).

**Example**
```
$.jforrst.getPostsShow(161803, function(data){
    var html = [];

    $('#postById a:first').attr('href', data.resp.post_url);
    $('#postById img').attr('src', data.resp.multiposts[1].snaps.mega_url);
    $('#postById h3').text(data.resp.title);
    $('#postById h4').html('by <a href="' + data.resp.user.url + '">' + data.resp.puser.name + '</a>');

    html.push('<li><b>Views:</b> ' + data.resp.view_count + '</li>');
    html.push('<li><b>Likes:</b> ' + data.resp.like_count + '</li>');
    html.push('<li><b>Comments:</b> ' + data.resp.comment_count + '</li>');

    $('#postById ul').html(html.join(''));
                });    
```
