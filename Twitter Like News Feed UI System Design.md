Here we are going to HLS for Twitter like News Feed System.

**1. Requirement**

- It should loaded from top-bottom
- Infinity number of Stories I can scroll
- Support Image / Video per story
- User can add Comments under the Story

**Non- Functional Requirement**

- Should be responsive
- Optimization over all + image
- Offline Support


**2. Mock Up UI**

![Mock Up UI for the news](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/25q20556ki4crbe54hm0.png)

- As we need to achieve infinity scrolle
- we can use virtualization technique
- we will have 2 observers (Top and Bottom)
- and based on the intersection we will call API for the data.
- We need to maintain Position absolute and calculate height for arranging the stories
- We need to adjust the scroll position

NOTE:- We can also use alternate approach like
react-window and react-virtualized
https://www.npmjs.com/package/react-virtualized

**3. Schema / State**

``` json

Stories: {
id: {
  id: string;
  message: string;
  articleLink: string;
  imageLinks: Array<string>
 }
}

comments: {
id: {
  comment: string
  likes: number;
  likeType: string
 }
}
```

**4. API**

1. getStories 
   payload:
  - pageno
  - limit

getComments: 
  payload: [ids]


**5. Real Time / Fetching Data**

- Pooling (long / short)
   - while using pooling, we can use requestAnimationFrame to optimize when user is not in active tab.
   - We can use Exponential error fallback retry when error happen 
- Http2/Push
- Socket.io/ web sockets
- server sent Events
- lets say user scroll and reach to the bottom Observer then we will call API to get the data.

**6. Search For Story**

- We need to use debounce/ Throttling for optimized search calls.
- we can use filters to narrow down the search.
- we can use **;** for searching multiple information

**Optimization**

**7. Networking**

- We can migrate to http/2, there we can send multiple requests in same time.
- then use can use bundle splitting (name.module.css)
- dynamic imports would have split into a bundle
- we can use defer the not immediately needed scripts
- we can use preload/prefetch attributes in CSS loading
- assets from CDN
- image lazy loading 
- Compress image

**8. Rendering**

- Is always better to have a constant no of nodes
- No Height and width change dynamically, if we do so then the layout will shift then it is a CPU-intensive job.
- Animation use transform (GPU) calculation
- Checking lighting tools for web vitals and based on the result we can optimize further
- Flattern CSS selector, rather than deep nested CSS selectors better to give it a class name and then use it.
- Initial loading placeholder

**9. Javascript**

- For heavy / CPU intensive works we can add webworks to do the job
- we can use dynamic loading + lazy + suspense 
- We can use Async Storage like index DB 
- We will have service worker enabled with index DB we can achieve Offline support.
- We can add a Background sync mechanism.
