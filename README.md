# so-docs-tools
A collection of scripts to use the data dump from Stack Overflow's dearly departed Documentation feature.

Pour one out for [Stack Overflow Documentation](https://meta.stackoverflow.com/questions/354217/sunsetting-documentation) and then grab [the data dump](https://archive.org/details/documentation-dump.7z). With a JSON parser in hand, you can use that content wherever your dreams take you. Just be sure to [provide proper attribution](https://meta.stackoverflow.com/questions/355115/documentation-is-read-only-what-s-next).

The currently available examples are:

* [`get-archive.rb`](https://github.com/jericson/so-docs-tools/blob/master/examples/get-archive.rb)&mdash;Downloads the archive and extracts it's contents. You only need to do this once.
* [`example2html.rb`](https://github.com/jericson/so-docs-tools/blob/master/examples/example2html.rb)&mdash;Extract the HTML representation of an example. To see what this looks like, I made a copy of [Creating and Initializing Arrays](http://jericson.github.io/docs/java/creating-java-arrays.html) in Java.
* [`attribution2wbm.rb`](https://github.com/jericson/so-docs-tools/blob/master/examples/attribution2wbm.rb)&mdash;Submits example or topic attribution to the Wayback Machine.
* [`submit2wbm.rb`](https://github.com/jericson/so-docs-tools/blob/master/examples/submit2wbm.rb)&mdash;a Ruby script that submits all topics to the [Internet Archive Wayback Machine](https://web.archive.org/). Demonstrates how to use `doctags.json` and `topics.json`. (I ran it on August 16, 2017 after Documentation was put in readonly mode. There's probably no reason to run it again. Also, it doesn't work for C# as `c%23` isn't allowed in their URLs.)
* Stay tuned for other exciting scripts!<sup>*</sup>

## Contributions welcome

I'm working with Ruby, but I'm happy to accept scripts written in other languages as long as I can test them out. I'm also happy to include links to other project using Documentation archive in this README. Feel free to submit pull requests and I'll incorporate them as quickly as I can.

If there's something you'd like to see from the archive and can't figure out how to extract the content, feel free to [add an issue](https://github.com/jericson/so-docs-tools/issues) or [ask on Meta Stack Overflow](https://meta.stackoverflow.com/questions/ask?tags=documentation,discussion,archive).

## Bugs

[![Build Status](https://travis-ci.org/jericson/so-docs-tools.svg?branch=master)](https://travis-ci.org/jericson/so-docs-tools)

* Tests are fragile. Changing the way these scripts work in even minor ways will break the tests. (Fortunately, the tests are also simple, so changing the expected `md5` hash result usually suffices.)
* The test framework also pulls in the entire archive from Archive.org and doesn't clean it up. This might be considered a feature by some.
* Getting user's display names requires a call to the [Stack Exchange API](http://api.stackexchange.com/docs/users-by-ids), which is subject to [rate limiting](http://api.stackexchange.com/docs/throttle). The method does not check to see if it's used the daily quota. Nor does it cache results. So it's easy to be throttled if you aren't careful. It also is a leading cause of failure for Travis CI Continuous Integration tests.
* The Stack Exchange API only returns 100 user IDs per page. I haven't yet added code to look at subsequent pages. Any user after the 100<sup>th</sup> will be listed in `userX` form as that's the default.
* My code more or less reproduces a RDBMS&mdash;poorly. It would probably be smarter to load the JSON files into SQLite or something.

---
Footnote:

\* Offer contingent on author's creativity and reader's ability to be excited.
