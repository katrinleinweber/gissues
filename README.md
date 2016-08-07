# Gissues
**[Github Repo](https://github.com/DeveloperMal/gissues/)**

**[PyPI](https://pypi.python.org/pypi/gissues/)**


![Gissue List](https://s8.postimg.org/rwxz5sffp/Gissues_List.png)

Gissues is the tool that helps developers view and manage github issues on the command line. 
Unlinke other github clients Gissues focuses on one thing and one thing only. Issues. 

# Installing

**Prerequisites**

Make sure you have the following installed:
- Python 3
- Pip

Install Gissues from pip with:

````
pip install gissues
```

# Basic Usage

The following section will show the basics of using Gissues. To view a complete list of avaiable commands please
run:

```
giss --help
```

## Viewing Issues

There are two ways to view issues in Gissues. You can view a list of a repo's issues with the `list` command. 
You can view an individual issues with the `show` command.

```
$> giss kennethreitz/requests list

== PAGE 1 OUT OF 10 ==== kennethreitz/requests ==
<open>[#3467] cannot pass realm parameter to HTTPDigestAuth
BY: alextorex0 [08/02/16 @ 13:57]
COMMENTS: 13
TAGS: 


<open>[#3463] #3416 persisting cookie policy.
BY: nateprewitt [07/30/16 @ 20:51]
COMMENTS: 1
TAGS: 


<open>[#3417] raise InvalidHeader on multiple Location values
BY: nateprewitt [07/15/16 @ 05:42]
COMMENTS: 8
TAGS: 


<open>[#3416] Unable to override cookie policy in Session.prepare_request
BY: bdusell [07/15/16 @ 05:20]
COMMENTS: 8
TAGS: 


<open>[#3367] Special IP proxy service timeout problems
BY: toadzhou [06/30/16 @ 07:26]
COMMENTS: 18
TAGS: 


== PAGE 1 OUT OF 10 ==== kennethreitz/requests ==

```

The `show` commands will display the issue with the issue number you provide

```
$> giss kennethreitz/requests show 2002


==================================================

<OPEN>[#2002] bool(failure response) is False
BY: slinkp [04/14/14 @ 21:09]
--------------------------------------------------

This is rather surprising, and not documented that I've seen (though I could certainly have missed it):
 

>>> r = requests.request('get', 'http://google.com/aopsdufsaf')
>>> r
<Response [404]>
>>> bool(r)
False

To me, "failure = false" is neither intuitive nor expected.

--------------------------------------------------
20 COMMENTS ...
==================================================

```

## Managing Issues

### Opening and Closing Issues

To open or close issues you can use the `open` and `close` commands respectively. Just provide the issue number.

```
$> giss DeveloperMal/gissues close 2

Are you sure you want to CLOSE this issue (Y/N): y
*** Closing issue number [#2]...
*** Issue [#2] is now CLOSED
```
```
$>  giss DeveloperMal/gissues open 2

Are you sure you want to OPEN this issue (Y/N): y
*** Reopening issue number [#2]...
*** Issue [#2] is now OPEN

```

### Creating and Editing Issues

Create a new issue with the `make` command. You will write the issue's body with the `nano` text editor.
Issue should be given a title. 

```
$> giss DeveloperMal/gissues make 

Type in a TITLE for issue: Improve Docs
Creating Issue For: 'Improve Docs'
Creating Issue...


 **** NEW ISSUE CREATED: [#3] 'Improve Docs' @ https://github.com/DeveloperMal/gissues/issues/3

```

To edit an existing issue use the `edit` command. It will allow you to edit the issue with the issue number you provide. 
Editing of the issue body will be done in the `nano` text editor.

```
$> giss DeveloperMal/gissues edit 2

Now editing body for [#2] 'There needs to be more info in readme'...
 **** Issue [#2] 'There needs to be more info in readme has been EDITED 
      @ https://github.com/DeveloperMal/gissues/issues/2

```

### Commenting on Issues

Gissues' `comment` commands allows you to comment on an issue and view comments on an issue. You will make a comment on the issue with the issuenumber you provide. When making a new comment the body of the comment will be written with the `nano` text editor. 

```
$> giss DeveloperMal/gissues comment 2

Now creating comment on issue [#2] 'There needs to be more info in readme'...
 **** Comment Successfully CREATED for [#2] 'There needs to be more info in readme'...

```

To view comments on an issue use the `-s` or `--show` flag on the `comment` command.

```
$> giss kennethreitz/requests comment 3296 -s

== PAGE 1 OUT OF 2 ==== kennethreitz/requests ==

--------------------------------------------------
[Lukasa commented 06/09/16 @ 08:10]
What version of requests are you using?
--------------------------------------------------


--------------------------------------------------
[Gaasmann commented 07/04/16 @ 13:12]
Hello,
Requests version is 2.7.0.
Thanks
--------------------------------------------------


--------------------------------------------------
[Lukasa commented 07/04/16 @ 13:30]
Cool, that's a good spot.

Yes, there is a minor bug in `resolve_redirects`. Specifically, while `resolve_redirects` attempts to remove proxy information, it cannot actually tell the difference between a proxy that was passed in via the command-line API or from the session and one that was extracted from the environment. This is because `resolve_redirects` is passed the *computed* `proxies` argument, not the *user's* `proxies` argument.

With the way the code in requests is structured, this is a very difficult problem to solve. One option is to hang the original `proxies` kwarg off the `Request` object: this will allow `rebuild_proxies` to essentially re-calculate the proxies argument. Another option is to suggest that the `NO_PROXY` environment variable overrides the user proxies argument for redirects: this is out of line with what we normally do, so I'm inclined to not do this. A third option is to try to do something wacky with storing the original `proxies` kwarg value and passing it to `Session.send` so that we can pass it to `resolve_redirects`, but that seems kind of nutty.

Does anyone else have an opinion on how to go about doing this that doesn't suck as much as the three I have just mentioned? @sigmavirus24?
--------------------------------------------------


--------------------------------------------------
[Lukasa commented 07/04/16 @ 13:36]
For what it's worth, I'd argue that this is a good indication that `proxies` (and probably `verify` and `cert`) are being handled at the wrong level of abstraction. Arguably, the core logic about deciding which proxy to use (and, by analogy, how to work the TLS) belongs more on Transport Adapters than on Sessions: it's a property of the connection, not a property of the HTTP layer.

We can fix that up, but it requires a breaking change in 3.0.0, which is...less than ideal.
--------------------------------------------------


--------------------------------------------------
[sigmavirus24 commented 07/04/16 @ 14:18]
What if Request/PreparedRequest objects had hidden state about session level settings and per-request level settings (which I think you're referring to as "user" settings) so that we could distinguish the two? Storing there, means allowing the TransportAdapter to resolve things would be (maybe?) a simpler change.
--------------------------------------------------

== PAGE 1 OUT OF 2 ==== kennethreitz/requests ==

```

# License

You are free to copy, modify, and distribute Gissues with attribution under the terms of the MIT license. See the LICENSE file for details.
