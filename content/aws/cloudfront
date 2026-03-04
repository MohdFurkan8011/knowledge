### CloudFront

- Cloud frontis a global service
- Amazon cloudfront is a webservices that speeds up distribution of your static and dynamic web content, such as .html, .css, .js and image files to users.
- Cloudfront delivers your content through a worldwide network of data centers called Edge locations.
- When a user request content that you are serving with coludfront, the user is routed(via DNS resolution) to the edge location that provides the lowest latency so that content is delivered with the best performance.
- If the content s already in the edge location with the lowest latency, cloudfront delivers it immediately.
- This dramatically reduces the number of network that your user's request must pass through which improves performance.
- If not, cloudfront retceives it from an amazon s3 bucket or an http/webservers that you have identified as the sorce for the definitive version of your content from origin servers.
- Cloudfront also keeps persistent connection with origin servers so file are fetched from the origin as quickly as possible.

**We can acces Amazon CloudFront in the following ways**
1. AWS management console
2. AWS SDK
3. Cloudfront API
4. AWS command line interface

**Cloudfront edge locations**
- Edge locations are not tied to availability zones or regions
- Amazon coludfront has 216 points of presence - 205 edge location and 11 regional edge caches in 84 cities across 42 countries.

**Cloudfront Regional Edge cache**
- Amazon cloud front has added several regional edge cache location globally at close proximity to your viewers.
- They are located between your origin webserver and the global edge locations that serve content directly to your viewer
- As objects become less popular, individual edge locations may remove these objects to make room for popular content.
- Regional edge cache working as a alternative of origin to reduce the burden of origin.
- Regional edge cache have a large cache width than any individual edge location, so object remains in the cache longer at the nearest regional edge caches.

**Cloudfront regional edge cache working**
- When a viewer makes a request on your website or through your applications, DNS routes the request to the cloud front edge location that can best serve the user's request.
- This location is typically the nearest cloudfront edge location in terms of latency.
- In the edge location, cloudfront checks its cache for the requested files.
- If the files are in the cache, cloudfront returns them to the user.
- If the files are not in the cache, the edge servers go to the nearest regional edge cache to fetch the object.
- Regional edge caches have feature panity with edge locations for eg. a cache invalidation request removes an object from both edge caches and regional edge cache before it expires.
- The next time a viewer request the object, cloudfront returns to the origin to fetch the latest version of the object.
- Proxy method PUT/POST/PATCH/OPTIONS/DELEE go directly to the origin from the edge locations and do not proxy through the regional edge caches.
- Dynamic content as determined at request time, does not flow through origin edge cache, but goes directly to the origin.