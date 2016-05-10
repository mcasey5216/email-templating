# Email Templating

note: some of this content is specific to the needs and application of UIE.

## Understanding Emails

![email clients](/images/demystifying-email-rendering.png)
Graphic of different email clients. ([source](http://webdesign.tutsplus.com/tutorials/what-you-should-know-about-html-email--webdesign-12908))

But these are the most common

Mobile clients
- Android 2.3 & 4.0
- iPhone 5  iOS 6
- iPhone 4S  iOS 6
- iPhone 3GS  iOS 5
- iPad 2  iOS 6
- BlackBerry OS 4 & 5
- Symbian S60
- Windows Phone 7.5

Desktop clients
- Apple Mail 4, 5, 6
- Lotus Notes 8.5
- Lotus Notes 8
- Thunderbird
- Windows Live Mail
- Outlook 2013
- Outlook 2011 for Mac
- Outlook 2010
- Outlook 2007
- Outlook 2003
- Outlook 2002/XP
- Outlook 2000

Webmail clients
- AOL Mail (on any browser)
- Gmail (on any browser)
- Outlook.com (on any browser)
- Yahoo! (on any browser)

### Standard Practices

 All emails must start as such

       <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
      <html xmlns="http://www.w3.org/1999/xhtml">
      <head>
      <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
      <title></title>
      <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
      </head>

This sets the stage for the email templates.  A detailed description of why can be found [here](http://webdesign.tutsplus.com/tutorials/what-you-should-know-about-html-email--webdesign-12908).

The `div`, `section`, and `article` tags are not supported in any reliable way.  Email templates should be built in nested tables since the `colspan` and `rowspan` attributes are not consistently supported.

Be careful with the inlining process.  Be sure to test every new email extensively, and run some preliminary checks on existing templates.

Some clients will strip certain tags, such as `h1`, `h2`, and `h3` (as well as `p` tags in some cases), so h tags are formatted as such: `<p class="h1"> ... </p>`.  When possible, simply skip the p tag altogether. Example

      <tr>
        <td style=“font-size: 12px; font-family: Arial, sans-serif; color: #666666;”>
          Text
        </td>
      </tr>

You can not use shorthand `CSS` styles for things like `border`, `font`, or `padding`.  

      table {
        padding: 10px 20px 10px;
      }

becomes:

      table {
        padding-top: 10px
        padding-bottom: 10px
        padding-right: 20px
        padding-left: 20px
      }
## Original Objectives

- Make a general template that is easy to reuse and responsive
- Create emails in a compiler language
  - Store the copy in variables
  - Read straight from markdown
  - Clarity in readability
  - If statements for conditional formatting
- Consistency and overlap with UIE pages (create/adopt P&SL)

### Step 1 - Standardization
The first step was to create a standard email in plain `HTML` that is responsive w/o media queries.

- sample can be found in `template/template.html` and the inline versions is located at `template/template-inline.html`

The problems that remain with just a plain `HTML` template?

- Code can get dense once customized - difficult to read
- Difficult to reuse customized code - usually easier to start from scratch
- Prone to mistakes
- Manual adjustments for edge cases
- Doesn’t read markdown

### Step 2 - HTML Alternative

Find an alternative to plain `HTML` that is still easy to convert back once its ready to be deployed (specifically through MailChimp).  A proposed solution is to use `Jade`, a clean whitespace-sensitive template language for writing `HTML`.  Benefits of `Jade` include:

- Better readability
- Partials
- Variables
- If statements
- Reading/compiling Markdown

It has the potential to make the code easily reusable, and less prone to mistakes/bugs.

## Possible Phases

Phase 1: Creating a library of parts

- Two and three column at different ratios, four columns
- Footers, headers, nested
- Separate and customized css libraries
- Create simple documentation on how to create new templates and use existing ones

Phase 2: Convert all our existing templates
- Make and test all of our existing ongoing email templates
	- Articles
	- Podcast
	- TotD
	- AYCL / VS
	- R+E

Phase 3: Minimizing CSS code / steps
- Creating Sass libraries
- Automate CSS inlining

(edit): CSS automation is replaced by styles stored in variables. Sass will probably not be necessary on this track.  4/21/16

Phase 4: Develop an Interface
- Form fields
- Read markdown from a file (not copy/paste)
- Interact with blogs and uie.com to capture information (totd, article)
	- Live updates before email and blog posts
