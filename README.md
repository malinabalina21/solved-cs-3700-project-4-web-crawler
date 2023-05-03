Download Link: https://assignmentchef.com/product/solved-cs-3700-project-4-web-crawler
<br>
This assignment is intended to familiarize you with the HTTP protocol. HTTP is (arguably) the most important application level protocol on the Internet today: the Web runs on HTTP, and increasingly other applications use HTTP as well (including Bittorrent, streaming video, Facebook and Twitter’s social APIs, etc.).

Your goal in this assignment is to implement a web crawler that gathers data from a fake social networking website that we have set up. The site is available here: <a href="http://fring.ccs.neu.edu/">Fakebook</a>.

<h3>What is a Web Crawler?</h3>

A web crawler (sometimes known as a robot, a spider, or a screen scraper) is a piece of software that automatically gathers and traverses documents on the web. For example, lets say you have a crawler and you tell it to start at www.wikipedia.com. The software will first download the Wikipedia homepage, then it will parse the HTML and locate all hyperlinks (i.e. anchor tags) embedded in the page. The crawler then downloads all the HTML pages specified by the URLs on the homepage, and parses them looking for more hyperlinks. This process continues until all of the pages on Wikipedia are downloaded and parsed.

Web crawlers are a fundamental component of today’s web. For example, Googlebot is Google’s web crawler. Googlebot is constantly scouring the web, downloading pages in search of new and updated content. All of this data forms the backbone of Google’s search engine infrastructure.

<h3>Fakebook</h3>

We have set up a fake social network for this project called <a href="http://fring.ccs.neu.edu/">Fakebook</a>. Fakebook is a very simple website that consists of the following pages:

<ul>

 <li><strong>Homepage</strong>: The Fakebook homepage displays some welcome text, as well as links to several random Fakebook users’ personal profiles.</li>

 <li><strong>Personal Profiles</strong>: Each Fakebook user has a profile page that includes their name, some basic demographic information, as well as a link to their list of friends.</li>

 <li><strong>Friends List</strong>: Each Fakebook user is friends with one or more other Fakebook users. This page lists the user’s friends and has links to their personal profiles.</li>

</ul>

To browse Fakebook, you must first login with a username and password. We will email each student to give them a unique username and password.

<h4>DO NOT TEST YOUR CRAWLERS ON PUBLIC WEBSITES</h4>

Many web server administrators view crawlers as a nuisance, and they get very mad if they see strange crawlers traversing their sites. <strong>Only test your crawler against Fakebook. Do not test it against any other website. </strong>

<h3>High Level Requirements</h3>

Your goal is to collect 5 <em>secret flags</em> that have been hidden somewhere on the Fakebook website. The flags are unique for each student, and the pages that contain the flags will be different for each student. Since you have no idea what pages the secret flags will appear on, and the Fakebook site is very large (tens of thousands of pages), your only option is to write a web crawler that will traverse Fakebook and locate your flags. If you chose to work in a team, you must submit the flags for every member on the team to qualify to receive full points.

Your web crawler must execute on the command line using the following syntax:

./webcrawler [username] [password]

username and password are used by your crawler to log-in to Fakebook. You may assume that the root page for Fakebook is available at <a href="http://fring.ccs.neu.edu/fakebook/">http://fring.ccs.neu.edu/fakebook/</a>. You may also assume that the log-in form for Fakebook is available at <a href="http://fring.ccs.neu.edu/accounts/login/?next=/fakebook/">http://fring.ccs.neu.edu/accounts/login/?next=/fakebook/</a>.

Your web crawler should print <strong>exactly fives lines of output</strong>: the five <em>secret flags</em> discovered during the crawl of Fakebook. If your program encounters an unrecoverable error, it may print an error message before terminating. Secret flags may be hidden on any page on Fakebook, and their exact location on each page may be different. Each secret flag is a 64 character long sequences of random alphanumerics. All secret flags will appear in the following format to make them easier to identify:

&lt;h2 class=’secret_flag’ style=”color:red”&gt;FLAG: 64-characters-of-random-alphanumerics&lt;/h2&gt;

<h3>Language</h3>

You can write your code in whatever language you choose, as long as your code compiles and runs on <strong>unmodified</strong> Khoury College Linux machines <strong>on the command line</strong>. Do not use libraries that are not installed by default on the Khoury College Linux machines, or that are disallowed for this project. You may use IDEs (e.g. Eclipse) during development, but make sure you code has <strong>no dependencies</strong> on your IDE and do not turn in your project without a Makefile.

<h3>HTTP and Libraries</h3>

<strong>All HTTP request and response code must be written from scratch.</strong> You need to implement creating and sending HTTP requests and parse HTTP responses. You may use any libraries available on login.khoury.neu.edu to create socket connections, parse URLs, and parse HTML. However, you may not use <strong>any</strong> libraries/modules/etc. that implement HTTP or manage cookies for you.

The following libraries are known to be legal/illegal in the context of this assignment:

<ul>

 <li>Legal

  <ul>

   <li>Python

    <ul>

     <li><em>socket</em></li>

     <li><em>parseurl</em></li>

     <li><em>html</em></li>

     <li><em>html.parse</em></li>

     <li><em>urllib.parse</em></li>

     <li><em>xml</em></li>

    </ul></li>

  </ul></li>

 <li>Illegal

  <ul>

   <li>Python

    <ul>

     <li><em>urllib</em></li>

     <li><em>urllib2</em></li>

     <li><em>html5lib</em></li>

     <li><em>httplib</em></li>

     <li><em>lxml</em></li>

     <li><em>requests</em></li>

     <li><em>pycurl</em></li>

     <li><em>cookielib</em></li>

     <li><em>BeautifulSoup</em></li>

    </ul></li>

   <li>Java

    <ul>

     <li><em>java.net.CookieHandler</em></li>

     <li><em>java.net.CookieManager</em></li>

     <li><em>java.net.HttpCookie</em></li>

     <li><em>java.net.HttpUrlConnection</em></li>

     <li><em>java.net.URLConnection</em>(Note that this includes <em>java.net.URL::openConnection</em> and <em>java.net.URL::openStream</em>)</li>

     <li><em>java.net.URL::getContent</em></li>

     <li><em>Jsoup</em></li>

    </ul></li>

  </ul></li>

</ul>

Please post any questions about the legality of any libraries to Piazza. It is much safer to ask ahead of time, rather than turn in code that uses a questionable library and receive points off for the assignment after the fact.

<h3>Implementation Details and Hints</h3>

In this assignment, your crawler must implement HTTP/1.1 (not 0.9 or 1.0). This means that there are certain HTTP headers like <em>Host</em> that you must include in your requests (i.e. they are required for all HTTP/1.1 requests). We encourage you to implement <em>Connection: Keep-Alive</em> (i.e. pipelining) to improve your crawler’s performance (and lighten the load on our server), but this is not required, and it is tricky to get correct. We also encourage you to implement <em>Accept-Encoding: gzip</em> (i.e. compressed HTTP responses), since this will also improve performance for everyone, but this is also not required. If you want to get crazy, you can definitely speed up your crawler by using multithreading or multiprocessing, but again this is not required functionality.

One of the key differences between HTTP/1.0 and HTTP/1.1 is that the latter supports <em>chunked encoding</em>. HTTP/1.1 servers may break up large responses into chunks, and it is the client’s responsibility to reconstruct the data by combining the chunks. Our server may return chunked responses, which means your client must be able to reconstruct them. To aid in debugging, you might consider using HTTP/1.0 for your implementation. Once you have a working 1.0 implementation, you can switch to 1.1 and add support for chunked responses.

In order to build a successful web crawler, you will need to handle several different aspects of the HTTP protocol:

<ul>

 <li>HTTP GET – These requests are necessary for downloading HTML pages.</li>

 <li>HTTP POST – You will need to implement HTTP POST so that your code can login to Fakebook. As shown above, you will pass a username and password to your crawler on the command line. The crawler will then use these values as parameters in an HTTP POST in order to log-in to Fakebook.</li>

 <li>Cookie Management – Fakebook uses cookies to track whether clients are logged in to the site. If your crawler successfully logs in to Fakebook using an HTTP POST, Fakebook will return a session cookie to your crawler. Your crawler should store this cookie, and submit it along with each HTTP GET request as it crawls Fakebook. If your crawler fails to handle cookies properly, then your software will not be able to successfully crawl Fakebook.</li>

</ul>

In addition to crawling Fakebook, your web crawler must be able to correctly handle <a href="https://en.wikipedia.org/wiki/List_of_HTTP_status_codes">HTTP status codes</a>. Obviously, you need to handle 200, since that means everything is okay. Your code must also handle:

<ul>

 <li>301 – Moved Permanently: This is known as an HTTP redirect. Your crawler should try the request again using the new URL given by the server in the <em>Location</em> header.</li>

 <li>403 – Forbidden and 404 – Not Found: Our web server may return these codes in order to trip up your crawler. In this case, your crawler should abandon the URL that generated the error code.</li>

 <li>500 – Internal Server Error: Our web server may <strong>randomly</strong> return this error code to your crawler. In this case, your crawler should re-try the request for the URL until the request is successful.</li>

</ul>

I highly recommend the <a href="http://www.jmarshall.com/easy/http/">HTTP Made Really Easy</a> tutorial as a starting place for learning about the HTTP. Furthermore, the developer tools built-in to Chrome and Firefox are both excellent for inspecting and understanding HTTP requests.

In addition to HTTP-specific issues, there are a few key things that all web crawlers must do in order function:

<ul>

 <li><strong>Track the Frontier</strong>: As your crawler traverses Fakebook it will observe many URLs. Typically, these uncrawled URLs are stored in a queue, stack, or list until the crawler is ready to visit them. These uncrawled URLs are known as the frontier.</li>

 <li><strong>Watch Out for Loops</strong>: Your crawler needs to keep track of where it has been, i.e. the URLs that it has already crawled. Obviously, it isn’t efficient to revisit the same pages over and over again. If your crawler does not keep track of where it has been, it will almost certainly enter an infinite loop. For example, if users A and B are friends on Fakebook, then that means A’s page links to B, and B’s page links to A. Unless the crawler is smart, it will ping-pong back and forth going A-&gt;B, B-&gt;A, A-&gt;B, B-&gt;A, …, etc.</li>

 <li><strong>Only Crawl The Target Domain</strong>: Web pages may include links that point to arbitrary domains (e.g. a link on google.com that points to cnn.com). <strong>Your crawler should only traverse URLs that point to pages on fring.ccs.neu.edu</strong>. For example, it would be valid to crawl <em>http://fring.ccs.neu.edu/fakebook/018912/</em>, but it would not be valid to crawl <em>http://www.fakebook.com/018912/</em>. Your code should check to make sure that each URL is in the target domain before you attempt to visit it.</li>

</ul>

<h3>Logging in to Fakebook</h3>

In order to write code that can successfully log-in to Fakebook, you will need to reverse engineer the HTML form on the log-in page. <em>Carefully</em> inspect the form’s code. It is not be as simple as it initially appears. The key acronym to be on the lookout for is <em>CSRF</em>.