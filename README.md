# h1reports

This tool is intended for HackerOne researchers with a repository of reports who wish to keep copies locally for their own search, archive, and reuse purposes.

**Reminder - all undisclosed reports and private program names are NOT allowed to be disclosed. The author disclaims any and all misuse of this software.**

## How does it work?

This tool will use your HackerOne API key and the new Researcher API to do the following:

 * Download a list of all reports in your Inbox
 * Download the full data of each report
 * Download all referenced attachments of each report

From this information, it will build a local repository with a series of pages in Markdown syntax, suitable for browsing using a Markdown browser such as [Obsidian](https://obsidian.md/), or for publishing using Jekyll and Github Pages (please do not ever publish these publicly as any non-disclosed report or program name is covered by the NDA that you signed).

Additionally, several index pages are built containing aggregate information, circa 1990's era web sites :)

## Getting a HackerOne API Key

You will need to create a HackerOne researcher API key. Log into your HackerOne account and navigate to the following link: [https://hackerone.com/settings/api_token/edit](https://hackerone.com/settings/api_token/edit).

Click Generate API Token. Note down the API key as it will not be displayed again.

## WARNING (Authenticated Usage)
**THIS SCRIPT HANDLES YOUR H1 API KEY TOKEN WHICH ALLOWS ACCESS TO YOUR HACKERONE PRIVATE DATA AND THE PRIVATE DATA OF YOUR HACKERONE PROGRAMS. BECAREFUL WHEN HANDLING THIS KEY. THE AUTHORS ARE NOT LIABLE FOR ANY MISUSE OF THIS SCRIPT OR YOUR HACKERONE API KEY. PLEASE USE AT YOUR OWN RISK. DO NOT PUBLISH ANY CONTENT WITH HACKERONE PRIVATE PROGRAM DATA OR UNDISCLOSED REPORTS ON PUBLIC PROGRAMS.**

## Running the Script

This tool was tested using Python 3.x. Ensure required dependencies are installed by:

```
pip install -f requirements.txt
```

Next, you will invoke the tool as follows:

```
python -u h1reports -u <your h1 username> -a <your H1 API key>
```

Example:

```
python -u h1reports -u pmnh -a 8xh...
```

This will create a directory called `output` (the location can be overridden with the `-d` parameter) and you will see a series of log statements indicating that data is being retrieved from the HackerOne researcher API.

```
$ python -u h1reports -u pmnh -a 8xh...
 [+] Getting report 1328337
  [+] Downloading attachment 1434332
  [+] Fixing attachment reference {F1434332}
  [+] Generating Markdown
  ...
 [+] Getting report 1276703
  [+] Downloading attachment 1387433
  [+] Fixing attachment reference {F1387433}
  [+] Generating Markdown
 [+] Building program summary for (redacted)
 [+] Saving top index
```

Inside the `output` directory, you will see a top-level index called `index.md`, and a series of subdirectories, one for each program containing reports. Each program directory contains its own index (linked from the top-level index) as well as a subdirectory containing all attachments associated with the reports.

Please note for researchers with many reports, this may take quite some time, and consume a significant amount of disk space.

Note that reports will always be downloaded, but since attachments can't be changed, if they are already present on the filesystem, they will not be downloaded again. This will make successive runs generally much faster than the initial run.

If you encounter an error during a run and wish to resume, add the `--resume` option. This will skip downloading individual reports if they are already cached on the local filesystem.

## Customization

The markdown is generated with Jinja templates, you can customize the layout if you wish by editing the templates in the `templates` directory. If you do something really interesting please submit an issue :)

## Feedback

This is a new tool and I'm excited to contribute it to the community! Please contact me on Twitter [@h1pmnh](https://twitter.com/h1pmnh) for feedback

## Notes

 * This tool was not developed by or endorsed by HackerOne
 * Note that the researcher API will not return reports on which you were not the reporter - this includes collaborations and duplicates

