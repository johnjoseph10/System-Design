# Facebook News Feed

## Clarifying Questions to Ask

1. Are we dealing with just text or posts or? image or video?
2. How many users?  DAU?
3. Show numbe rof likes and comments for each post?
4. Scale of the system?



## Functional Requirements

1. Post a message
2. Follow or unfollow users
3. View friends feed

## Non functional Requirements

1. High Availability, Eventual consistency is ok 
2. Getting news feed should be quick ( less than  1-2 seconds)
3. Submit a post should immediately appear in the feed ( < 1s)
4. Support 2B users


## User Entities

1. Post (id, userid, text, mediaUrl, createdTs)
2. Feed
3. User (id, name, email, phone)
4. Follow

## API Design

1. POST /post/create  (userid/auth token: JWT )
{
    content : message/image/video
}
Response = postId;

2. GET /newsfeed  (userid: JWT ) 
{
    screenSize
    #ofPosts
    getFrom
}
=> List of POSTs

3. POST  /user/id/follow


## Capacity Design

Do it later


## Design Diagram

    








## Refrences:
https://systemdesignprep.com/newsfeed
https://www.hellointerview.com/learn/system-design/problem-breakdowns/fb-news-feed
