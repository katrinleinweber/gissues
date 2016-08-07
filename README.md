# Gissues
![Gissue List](https://s8.postimg.org/rwxz5sffp/Gissues_List.png)

Gissues is a tool that helps developers alike view and manage issues from github on the command line. Unlinke other github clients Gissues focuses on one thing and one thing only. Issues. 

# Installing

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

Create a new issues with the `make` command. You will write the issue's body with the `nano` text editor.
Issue should be given a title. 

```
$> giss DeveloperMal/gissues make 

Type in a TITLE for issue: Improve Docs
Creating Issue For: 'Improve Docs'
Creating Issue...


 **** NEW ISSUE CREATED: [#3] 'Improve Docs' @ https://github.com/DeveloperMal/gissues/issues/3

```
