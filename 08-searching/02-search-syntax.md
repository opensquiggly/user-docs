---
Order: 2
Title: Search Syntax
---
# Form of a Search Expression

We recommend that you start by putting the regex pattern that you want to use to match
the document content first, followed by any search filtering options:

##### Recommended: Content search pattern followed by options
```
regex_to_match_doc_content_here [options]
```

Legally speaking, we don't require options to come after the content pattern. You can
put options before and after the content expression, though we don't recommend it.

##### Legal but not recommended:

```
[options] regex_to_match_doc_content_here [more_options]
---------                                 --------------
    ^                                            ^
    |                                            |
    +--------------------+-----------------------+
                         |
                         |
          Options can come both before and after
          the content search pattern
```

The content search pattern must be contiguous.

##### Should be illegal:

```
[options] content_pattern_part_1 [more_options] content_pattern_part_2  
          ----------------------                ----------------------
                    ^                                       ^
                    |                                       |
                    +------------------+--------------------+
                                       |
                                       |
                     This should be illegal because the two content sections
                     are discontinguous. However, I think there are some
                     bugs in this area and we're not currently catching this.                                              
```

# Regular Expressions Pattern vs. Keyword Patterns

Currently all searches are interpreted as regular expressions, regardless of whether or
not the ".*" button is checked (the little box immediately following the search input
in the header bar).

Search test cases should be written assuming regex. We will need to revisit our search
plans after we add keyword-based content searching.

# List of Search Options

The following search options are available. Note that some options can be specified
more than once. In these cases the options are cummulative and combined together
with an "and" boolean clause. I will discuss this momentarily.

<table>
  <tr>
    <th>Option Name</th>
    <th>Default Value</th>
    <th>Description</th>
  </tr>
  <tr>
    <th colspan="3">
      Settings Filters (Can be Specified Only Once)
    </th>
  </tr>
  <tr>
    <td nowrap><code>case:[yes|no]</code></td>
    <td>no</td>
    <td>
      Turns on case sensitive searching. By default searching should be case insensitive.
    </td>
  </tr>
  <tr>
    <td nowrap><code>count:nnn</code></td>
    <td>30</td>
    <td>
      Specifies the maximum number of search results to return in the results
      list.
    </td>
  </tr>
  <tr>
    <td nowrap><code>maxscale:nnn</code></td>
    <td>5</td>
    <td>
      Affects the maximum number of candidate documents that are searched.
    </td>
  </tr>
  <tr>
    <td nowrap><code>maxdocsize:nnn</code></td>
    <td>65535</td>
    <td>
      Documents bigger than this are skipped.
    </td>
  </tr>
  <tr>
    <td nowrap><code>includeskipped:[yes|no]</code></td>
    <td>no</td>
    <td>
      Whether or not large skipped document should be returned in the results list.
    </td>
  </tr>
  <tr>
    <td nowrap><code>timeout:nnn</code></td>
    <td>5</td>
    <td>
      Abort the search if it takes longer than nnn seconds.
    </td>
  </tr>
  <tr>
    <th colspan="3">
      Include/Exclude Filters (Can be Specified More than Once)
    </th>
  </tr>
  <tr>
    <td nowrap><code>doctype:[page|repo]</code></td>
    <td>N/A</td>
    <td>
      Include or exclude documents with a matching sourcetype. Sourcetype values
      can be one of the following:
      <table>
        <tr>
          <th>Name</th>
          <th>Description</th>
        </tr>
        <tr>
          <td><code>page</code></td>
          <td>
            Matches pages stored internally in the OpenSquiggly database (topic pages
            or journal pages).
          </td>
        </tr>
        <tr>
          <td><code>repo</code></td>
          <td>
            Matches content from files in mounted Git repositories.
          </td>
        </tr>
      </table>
    </td>
  </tr>
  <tr>
    <td nowrap><code>-doctype:[page|repo]</code></td>
    <td>N/A</td>
    <td>
      Excludes documents with a matching sourcetype.
    </td>
  </tr>
  <tr>
    <td nowrap><code>file:regex_pattern</code></td>
    <td>N/A</td>
    <td>
      Include documents with filenames (or topic page titles) matching the 
      specified pattern. The pattern is a regex expression.
    </td>
  </tr>
  <tr>
    <td nowrap><code>-file:regex_pattern</code></td>
    <td>N/A</td>
    <td>
      Exclude documents with filenames (or topic page titles) matching the 
      specified pattern. The pattern is a regex expression.
    </td>
  </tr>
  <tr>
    <td nowrap><code>repo:regex_pattern</code></td>
    <td>N/A</td>
    <td>
      <p>
        Include documents with repository names matching the specified
        pattern. The pattern is a regex expression. Note, this is the full repository 
        name after the mount point's Git URL Pattern field has been fully evaluated 
        with all macros expanded.
      </p>
      <p>
        Also note that specifying this option implies <code>doctype:repo</code>
      </p>
    </td>
  </tr>
  <tr>
    <td nowrap><code>-repo:regex_pattern</code></td>
    <td>N/A</td>
    <td>
      <p>
        Exclude documents with repository names matching the specified
        pattern. The pattern is a regex expression.
      </p>
      <p>
        Also note that specifying this option implies <code>doctype:repo</code>
      </p>
    </td>
  </tr>
  <tr>
    <td nowrap><code>title:regex_pattern</code></td>
    <td>N/A</td>
    <td>
      Synoymous with the <code>file:regex_pattern</code> option.
    </td>
  </tr>
  <tr>
    <td nowrap><code>-title:regex_pattern</code></td>
    <td>N/A</td>
    <td>
      Synoymous with the <code>-file:regex_pattern</code> option.
    </td>
  </tr>
</table>


# Case Sensitivity

If <code>case:yes</code> is specified, the content is searched with case sensitivity in effect. Otherwise,
casing is ignored.

# Maximum Count

Specifies the maximum number of documents to find. The default is 30. Note that if a larger number is
specified, the search could take longer to complete. The user may want to increase the timeout setting
in conjunction.

# Document Type Inclusion or Exclusion

<code>doctype:[page|repo]</code><br>
<code>-doctype:[page|repo]</code>

With these options, you can narrow the search to include only pages (e.g., internally authored regular topic pages) or
repository-based content (e.g., content from mount points).

# Filename Inclusion or Exclusion

<code>file:regex_pattern</code><br>
<code>-file:regex_pattern</code>

With these options, you can include or exclude files based on their file names (or page title names).

### Example 1 : Include only files located in the components folder

```
file:/components/
```

### Example 2 : Include only files with an extension of ".js"

```
file:\.js$
```

### Example 3 : Include files with an extension of ".js" or ".svelte"

Here, we use the regex "or" capability which is done using the vertical bar (|) character.

```
file:\.js$|\.svelte$
```

### Example 4 : Include files in the components folder AND has an extension of ".js" or ".svelte"

If we specify multiple file filters, they are combined together using the "AND" boolean condition.

By using the regex vertical bar to specifies "ors", and using multiple file filters to specify "ands",
we can combine filters together to create complex conditions.

```
file:/components/ file:\.js$|\.svelte$
----------------- --------------------
       ^                    ^
       |                    |
  File must contain   File must end in either
  "/components/" in   ".js" or ".svelte"
  its path name             |
       |                    |
       +----------+---------+
                  |
                 AND (both subcontions must be true)
  
```

# Repository Name Inclusion or Exclusion

<code>repo:regex_pattern</code><br>
<code>-repo:regex_pattern</code>

With these options, the user can include or exclude results based on which repository it is in. These
options are particularly useful if you have attached many repositories in your account, and you want to
focus the search on only some of them.

### Example : Include only opensquiggly repositories, discard content from any other repository

```
repo:opensquiggly
```

As with the <code>file:regex_pattern</code> options, if multiple filters are specified, they are
combined together using the AND boolean condition (i.e., all conditions must be true, otherwise the
document is discarded from the search results).

# Title Inclusion or Exclusion

<code>title:regex_pattern</code><br>
<code>-title:regex_pattern</code>

These options are synonmous with the <code>file:regex_pattern</code> filter.

# Limiting the Number of Candidate Documents Searched

<code>maxscale:nnn</code>

To understand this option, you need to first understand a little bit about how we implement
regular expression searching.

Without any indexing strategy, we would have to search every document in the user's account to
determine whether or not it matched the regex expression. This could be very slow, especially if the
user creates many mount points within their account.

There is no known indexing strategy for regular expression documents that can quickly return only
the matching expressions. However, there is an indexing strategy called "trigram indexing" that can
be used to reduce the number of documents that need to be searched with the full regex expression.

We call the documents that match the trigram index "candidate documents". These are documents that "might"
match the regex. We can picture the workflow as follows:

```
+------------------------------+
| All Documents                |
+------------------------------+
             |
             v
+------------------------------+
| Trigram Index Query          |
+------------------------------+
             |
             v
+------------------------------+
| Candidate Documents          |
+------------------------------+
             |
             v
+------------------------------+
| Full Regex Search            |
+------------------------------+
             |
             v
+------------------------------+
| Final list of matching       |
| documents                    |
+------------------------------+                                                
```

Depending on the regex expression and the content of the documents in the user's database, we
may get a high or low percentage hit rate of Candidate Documents.

If the percentage hit rate is high, then we can quickly find documents up to the "count" number
that the user has asked for. A high percentage hit rate is good.

But sometimes the hit rate could be low. If the hit rate is too low, then we have to search through
many candidate documents to find the number of matching documents the user has asked for.

The <code>maxscale</code> setting controls how hard we try to find matches in the set of candidate
documents.

The default <code>maxscale</code> value is <code>5</code>. We use this value as a multiplier against
the <code>count</code> setting to determine the maximum number of candidate documents we will search. For example,
if the user has asked us to find 30 documents (the default <code>count</code> value), then we would search
up to 150 candidate documents to find the 30 matching documents. Note that because the setting is a multiple
of the count, it will automatically increase base on size. If the user asks for 100 matching documents and
leaves all other values at their default, then we would search up to 500 candidate documents to find 100
final matches.

An example of a search with a very low hit rate is:

```
for\s{10}this
```

This searches for the word "for", followed by exactly 10 spaces, followed by the word "this".

Since coding languages commonly contain the words "for" and "this", the candidate documents query will
contain a large subset of documents. However, virtually none of those document will contain exactly
10 spaces between the words "for" and "this", therefore we will get a very low hit rate (probably 0).

The user may want to increase this value if they have a low hit rate search and they want us to search
more than the usual number of candidate documents to find them. They might also want to increase the
timeout at the same time, since the search will take longer to search through more candidate documents.

Example:

```
for\s{10}this maxscale:10 timeout:20
```

# Maximum Document Size

<code>maxdocsize:nnn</code>

Regular expression searches in general are slow. The bigger the size of the document, the slower the
regex search will be.

To speed up the search, by default we skip searching any documents that are bigger than 65535 bytes (64K).

This is usually acceptable because developers generally try to keep their source code files to a few thousand
lines long or less. If the user wants us to search large documents, they can increase the <code>maxdocsize</code>.

# Include Skipped Documents Larger than the Maximum Size

<code>includeskipped:[yes|no]</code>

If a document was skipped as a result of it being larger than the <code>maxdocsize</code>, this setting
controls whether or not to include that skipped document in the result list.

The default value is <code>no</code>, meaning that large documents are not included in the final returned
results.

# Setting the Search Timeout

<code>timeout:nnn</code>

This setting increases the maximum time, in seconds, that the search will search for. If it hits the
timeout value, it will stop searching and return all the documents that were found up until that point.

The default value is <code>5</code> (seconds).

If you are asking for a large <code>count</code>, or you've increased your <code>maxscale</code> setting,
then you might consider increasing the <code>timeout</code> value to give the

Example:

```
foreach count:1000 timeout:20
```

# Finding Unreferenced pages

<code>ref:none</code>

This setting let's you find unreferenced pages in your document tree graph.

Recall from the page theory document, that documents within OpenSquiggly are connected together by a
graph of their table of contents references.

If a user has removed all references to a page, then it will not appear anywhere in the user's table
of contents starting from the user's Home page and drilling down into each inner page.

This setting gives the user a quick way to find their unreferenced pages. It's common for a user to
want to delete their unreferenced pages, because presumably the reason why they've removed any reference
to the page is because the page is no longer useful.

It's hard to find unreferenced pages because, well, they are unreferenced. This search allows you to
find them.

Note that this search relies on the <code>ReferencedBy</code> array stored in the database. There are
some known bugs in this area, so it is important to test the <code>ref:none</code> search to help
identify these bugs.
