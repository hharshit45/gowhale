## Guide for contribution
- git clone
- git commit -m"fdgjlk"
- harshit srivastava
## How to start with GoLang
- Introduction
C syntax
First, let’s talk about C syntax. C took an unusual and clever approach to declaration syntax. Instead of describing the types with special syntax, one writes an expression involving the item being declared, and states what type that expression will have. Thus

int x;
declares x to be an int: the expression ‘x’ will have type int. In general, to figure out how to write the type of a new variable, write an expression involving that variable that evaluates to a basic type, then put the basic type on the left and the expression on the right.

Thus, the declarations
The pointer in C language is a variable which stores the address of another variable. This variable can be of type int, char, array, function, or any other pointer. The size of the pointer depends on the architecture. However, in 32-bit architecture the size of a pointer is 2 byte.

int *p;
int a[3];
In C, we can divide a large program into the basic building blocks known as function. The function contains the set of programming statements enclosed by {}. A function can be called multiple times to provide reusability and modularity to the C program. In other words, we can say that the collection of functions creates a program. The function is also known as procedureor subroutinein other programming languages.

State that p is a pointer to int because ‘*p’ has type int, and that a is an array of ints because a[3] (ignoring the particular index value, which is punned to be the size of the array) has type int.

What about functions?
In C, we can divide a large program into the basic building blocks known as function. The function contains the set of programming statements enclosed by {}. A function can be called multiple times to provide reusability and modularity to the C program. In other words, we can say that the collection of functions creates a program. The function is also known as procedureor subroutinein other programming languages.

In c, we can divide a large program into the basic building blocks known as function. The function contains the set of programming statements enclosed by {}. A function can be called multiple times to provide reusability and modularity to the C program. In other words, we can say that the collection of functions creates a program. The function is also known as procedureor subroutinein other programming languages.

Advantage of functions in C
There are the following advantages of C functions.

By using functions, we can avoid rewriting same logic/code again and again in a program.
We can call C functions any number of times in a program and from any place in a program.
We can track a large C program easily when it is divided into multiple functions.
Reusability is the main achievement of C functions.
However, Function calling is always a overhead in a C program.

Originally, C’s function declarations wrote the types of the arguments outside the parens, like this:

int main(argc, argv)
    int argc;
    char *argv[];
{ /* ... */ }
Again, we see that main is a function because the expression main(argc, argv) returns an int. In modern notation we’d write

int main(int argc, char *argv[]) { /* ... */ }
but the basic structure is the same.

This is a clever syntactic idea that works well for simple types but can get confusing fast. The famous example is declaring a function pointer. Follow the rules and you get this:

int (*fp)(int a, int b);
Here, fp is a pointer to a function because if you write the expression (*fp)(a, b) you’ll call a function that returns int. What if one of fp’s arguments is itself a function?

int (*fp)(int (*ff)(int x, int y), int b)
That’s starting to get hard to read.

Of course, we can leave out the name of the parameters when we declare a function, so main can be declared

int main(int, char *[])
Recall that argv is declared like this,

char *argv[]
so you drop the name from the middle of its declaration to construct its type. It’s not obvious, though, that you declare something of type char *[] by putting its name in the middle.

And look what happens to fp’s declaration if you don’t name the parameters:

int (*fp)(int (*)(int, int), int)
Not only is it not obvious where to put the name inside

int (*)(int, int)
it’s not exactly clear that it’s a function pointer declaration at all. And what if the return type is a function pointer?

int (*(*fp)(int (*)(int, int), int))(int, int)
It’s hard even to see that this declaration is about fp.

You can construct more elaborate examples but these should illustrate some of the difficulties that C’s declaration syntax can introduce.

There’s one more point that needs to be made, though. Because type and declaration syntax are the same, it can be difficult to parse expressions with types in the middle. This is why, for instance, C casts always parenthesize the type, as in

(int)M_PI
Go syntax
Languages outside the C family usually use a distinct type syntax in declarations. Although it’s a separate point, the name usually comes first, often followed by a colon. Thus our examples above become something like (in a fictional but illustrative language)

x: int
p: pointer to int
a: array[3] of int
These declarations are clear, if verbose - you just read them left to right. Go takes its cue from here, but in the interests of brevity it drops the colon and removes some of the keywords:

x int
p *int
a [3]int
There is no direct correspondence between the look of [3]int and how to use a in an expression. (We’ll come back to pointers in the next section.) You gain clarity at the cost of a separate syntax.

Now consider functions. Let’s transcribe the declaration for main as it would read in Go, although the real main function in Go takes no arguments:

func main(argc int, argv []string) int
Superficially that’s not much different from C, other than the change from char arrays to strings, but it reads well from left to right:

function main takes an int and a slice of strings and returns an int.

Drop the parameter names and it’s just as clear - they’re always first so there’s no confusion.

func main(int, []string) int
One merit of this left-to-right style is how well it works as the types become more complex. Here’s a declaration of a function variable (analogous to a function pointer in C):

f func(func(int,int) int, int) int
Or if f returns a function:

f func(func(int,int) int, int) func(int, int) int
It still reads clearly, from left to right, and it’s always obvious which name is being declared - the name comes first.

The distinction between type and expression syntax makes it easy to write and invoke closures in Go:

sum := func(a, b int) int { return a+b } (3, 4)
Pointers
Pointers are the exception that proves the rule. Notice that in arrays and slices, for instance, Go’s type syntax puts the brackets on the left of the type but the expression syntax puts them on the right of the expression:

var a []int
x = a[1]
For familiarity, Go’s pointers use the * notation from C, but we could not bring ourselves to make a similar reversal for pointer types. Thus pointers work like this

var p *int
x = *p
We couldn’t say

var p *int
x = p*
because that postfix * would conflate with multiplication. We could have used the Pascal ^, for example:

var p ^int
x = p^
and perhaps we should have (and chosen another operator for xor), because the prefix asterisk on both types and expressions complicates things in a number of ways. For instance, although one can write

[]int("hi")
as a conversion, one must parenthesize the type if it starts with a *:

(*int)(nil)
Had we been willing to give up * as pointer syntax, those parentheses would be unnecessary.

So Go’s pointer syntax is tied to the familiar C form, but those ties mean that we cannot break completely from using parentheses to disambiguate types and expressions in the grammar.

Overall, though, we believe Go’s type syntax is easier to understand than C’s, especially when things get complicated.

Notes
Go’s declarations read left to right. It’s been pointed out that C’s read in a spiral! See The “Clockwise/Spiral Rule” by David Anderson.


## Getting started with servers and GoLang
Package http provides HTTP client and server implementations.

Get, Head, Post, and PostForm make HTTP (or HTTPS) requests:

resp, err := http.Get("http://example.com/")
...
resp, err := http.Post("http://example.com/upload", "image/jpeg", &buf)
...
resp, err := http.PostForm("http://example.com/form",
	url.Values{"key": {"Value"}, "id": {"123"}})
The client must close the response body when finished with it:

resp, err := http.Get("http://example.com/")
if err != nil {
	// handle error
}
defer resp.Body.Close()
body, err := io.ReadAll(resp.Body)
// ...
For control over HTTP client headers, redirect policy, and other settings, create a Client:

client := &http.Client{
	CheckRedirect: redirectPolicyFunc,
}

resp, err := client.Get("http://example.com")
// ...

req, err := http.NewRequest("GET", "http://example.com", nil)
// ...
req.Header.Add("If-None-Match", `W/"wyzzy"`)
resp, err := client.Do(req)
// ...
For control over proxies, TLS configuration, keep-alives, compression, and other settings, create a Transport:

tr := &http.Transport{
	MaxIdleConns:       10,
	IdleConnTimeout:    30 * time.Second,
	DisableCompression: true,
}
client := &http.Client{Transport: tr}
resp, err := client.Get("https://example.com")
Clients and Transports are safe for concurrent use by multiple goroutines and for efficiency should only be created once and re-used.

ListenAndServe starts an HTTP server with a given address and handler. The handler is usually nil, which means to use DefaultServeMux. Handle and HandleFunc add handlers to DefaultServeMux:

http.Handle("/foo", fooHandler)

http.HandleFunc("/bar", func(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello, %q", html.EscapeString(r.URL.Path))
})

log.Fatal(http.ListenAndServe(":8080", nil))
More control over the server's behavior is available by creating a custom Server:

s := &http.Server{
	Addr:           ":8080",
	Handler:        myHandler,
	ReadTimeout:    10 * time.Second,
	WriteTimeout:   10 * time.Second,
	MaxHeaderBytes: 1 << 20,
}
log.Fatal(s.ListenAndServe())
Starting with Go 1.6, the http package has transparent support for the HTTP/2 protocol when using HTTPS. Programs that must disable HTTP/2 can do so by setting Transport.TLSNextProto (for clients) or Server.TLSNextProto (for servers) to a non-nil, empty map. Alternatively, the following GODEBUG environment variables are currently supported:

GODEBUG=http2client=0  # disable HTTP/2 client support
GODEBUG=http2server=0  # disable HTTP/2 server support
GODEBUG=http2debug=1   # enable verbose HTTP/2 debug logs
GODEBUG=http2debug=2   # ... even more verbose, with frame dumps


Add a fuzz test
The unit test has limitations, namely that each input must be added to the test by the developer. One benefit of fuzzing is that it comes up with inputs for your code, and may identify edge cases that the test cases you came up with didn’t reach.

func FuzzReverse(f *testing.F) {
    testcases := []string{"Hello, world", " ", "!12345"}
    for _, tc := range testcases {
        f.Add(tc)  // Use f.Add to provide a seed corpus
    }
    f.Fuzz(func(t *testing.T, orig string) {
        rev := Reverse(orig)
        doubleRev := Reverse(rev)
        if orig != doubleRev {
            t.Errorf("Before: %q, after: %q", orig, doubleRev)
        }
        if utf8.ValidString(orig) && !utf8.ValidString(rev) {
            t.Errorf("Reverse produced invalid UTF-8 string %q", rev)
        }
    })
}
Fuzzing has a few limitations as well. In your unit test, you could predict the expected output of the Reverse function, and verify that the actual output met those expectations.
There are a few different ways you could debug this error. If you are using VS Code as your text editor, you can set up your debugger to investigate.

In this tutorial, we will log useful debugging info to your terminal.

First, consider the docs for utf8.ValidString.

ValidString reports whether s consists entirely of valid UTF-8-encoded runes.
The current Reverse function reverses the string byte-by-byte, and therein lies our problem. In order to preserve the UTF-8-encoded runes of the original string, we must instead reverse the string rune-by-rune.

To examine why the input (in this case, the Chinese character 泃) is causing Reverse to produce an invalid string when reversed, you can inspect the number of runes in the reversed string.

Like before, there are several ways you could debug this failure. In this case, using a debugger would be a great approach.

we will log useful debugging info in the Reverse function.

Look closely at the reversed string to spot the error. In Go, a string is a read only slice of bytes, and can contain bytes that aren’t valid UTF-8. The original string is a byte slice with one byte, '\x91'. When the input string is set to []rune, Go encodes the byte slice to UTF-8, and replaces the byte with the UTF-8 character �. When we compare the replacement UTF-8 character to the input byte slice, they are clearly not equal.

f.Fuzz(func(t *testing.T, orig string) {
    rev := Reverse(orig)
    doubleRev := Reverse(rev)
    t.Logf("Number of runes: orig=%d, rev=%d, doubleRev=%d", utf8.RuneCountInString(orig), utf8.RuneCountInString(rev), utf8.RuneCountInString(doubleRev))
    if orig != doubleRev {
        t.Errorf("Before: %q, after: %q", orig, doubleRev)
    }
    if utf8.ValidString(orig) && !utf8.ValidString(rev) {
        t.Errorf("Reverse produced invalid UTF-8 string %q", rev)
    }
})
=======
## further general information
Godoc extracts and generates documentation for Go programs.

It runs as a web server and presents the documentation as a web page.

godoc -http=:6060
Usage:

godoc [flag]
The flags are:

-v
	verbose mode
-timestamps=true
	show timestamps with directory listings
-index
	enable identifier and full text search index
	(no search box is shown if -index is not set)
-index_files=""
	glob pattern specifying index files; if not empty,
	the index is read from these files in sorted order
-index_throttle=0.75
	index throttle value; a value of 0 means no time is allocated
	to the indexer (the indexer will never finish), a value of 1.0
	means that index creation is running at full throttle (other
	goroutines may get no time while the index is built)
-index_interval=0
	interval of indexing; a value of 0 sets it to 5 minutes, a
	negative value indexes only once at startup
-play=false
	enable playground
-links=true
	link identifiers to their declarations
-write_index=false
	write index to a file; the file name must be specified with
	-index_files
-maxresults=10000
	maximum number of full text search results shown
	(no full text index is built if maxresults <= 0)
-notes="BUG"
	regular expression matching note markers to show
	(e.g., "BUG|TODO", ".*")
-goroot=$GOROOT
	Go root directory
-http=addr
	HTTP service address (e.g., '127.0.0.1:6060' or just ':6060')
-templates=""
	directory containing alternate template files; if set,
	the directory may provide alternative template files
	for the files in $GOROOT/lib/godoc
-url=path
	print to standard output the data that would be served by
	an HTTP request for path
-zip=""
	zip file providing the file system to serve; disabled if empty
By default, godoc looks at the packages it finds via $GOROOT and $GOPATH (if set). This behavior can be altered by providing an alternative $GOROOT with the -goroot flag.

When the -index flag is set, a search index is maintained. The index is created at startup.

The index contains both identifier and full text search information (searchable via regular expressions). The maximum number of full text search results shown can be set with the -maxresults flag; if set to 0, no full text results are shown, and only an identifier index but no full text search index is created.

By default, godoc uses the system's GOOS/GOARCH. You can provide the URL parameters "GOOS" and "GOARCH" to set the output on the web page for the target system.

The presentation mode of web pages served by godoc can be controlled with the "m" URL parameter; it accepts a comma-separated list of flag names as value:

all	show documentation for all declarations, not just the exported ones
methods	show all embedded methods, not just those of unexported anonymous fields
src	show the original source code rather than the extracted documentation
flat	present flat (not indented) directory listings using full paths
For instance, https://golang.org/pkg/math/big/?m=all shows the documentation for all (not just the exported) declarations of package big.

By default, godoc serves files from the file system of the underlying OS. Instead, a .zip file may be provided via the -zip flag, which contains the file system to serve. The file paths stored in the .zip file must use slash ('/') as path separator; and they must be unrooted. $GOROOT (or -goroot) must be set to the .zip file directory path containing the Go root directory. For instance, for a .zip file created by the command:

zip -r go.zip $HOME/go
one may run godoc as follows:

godoc -http=:6060 -zip=go.zip -goroot=$HOME/go
