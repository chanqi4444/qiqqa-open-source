
v82 release
===========

> ## Note
>
> This release is **binary compatible with v80 and v79**: any library created using this version MUST be readable and usable by v80 and v79 software releases.


* (acd9229) README: point at the various places where software releases are to be found.

* work done on run-time performance / reduce memory leaks. Code simplification.

* (305c085) fixes https://github.com/jimmejardine/qiqqa-open-source/issues/96 / https://github.com/jimmejardine/qiqqa-open-source/issues/98: correct deadlock prevention code in CitationManager. Code robustness.

* (6ef9b44) Code robustness. Refactoring the code and making its interface threadsafe. Fixes https://github.com/jimmejardine/qiqqa-open-source/issues/96 / https://github.com/jimmejardine/qiqqa-open-source/issues/106 / https://github.com/jimmejardine/qiqqa-open-source/issues/98.

* (6ef9b44) Tweak: `AddLegacyWebLibrariesThatCanBeFoundOnDisk()`: at startup, try to load all .known_web_libraries files you can find as those should provide better (= original) names of the various Commercial Qiqqa Web Libraries. (This is running ahead to the tune of https://github.com/jimmejardine/qiqqa-open-source/issues/109 / https://github.com/jimmejardine/qiqqa-open-source/issues/103)

* (8b90f41) Code robustness. Fix https://github.com/jimmejardine/qiqqa-open-source/issues/105 : turns out the config user GUID is NULL/not initialized at startup. This fix ensures there's a predictable (Guest) config active from the very start of the Qiqqa app.

* (d52d565) quick hack for https://github.com/jimmejardine/qiqqa-open-source/issues/104: make Qiqqa start no matter what.

* (f515ca7) "directory tree as tags" fix: recognize both \ and / as 'tag' separators in any document path.

* (626902b) (fix) Code robustness. Copy the new library background image file into place, if it is another file than the one we already have. Fix: do *not* delete the active image file when the user did not select another image file.

* (1b2daca) Performance / Code Robustness.
  - at very high loads allow the UI to update regularly while work is done in background tasks.
  - show mouse cursor as Hourglass/Busybee: during application startup, this is used to give visual feedback to the user that the work done is taking a while (relatively long startup time, particularly for large libraries which are auto-opened due to saved tab panel sets including their main library tabs)
  - fixed a couple of crashes.

* (fb775d5) Code Robustness. Take out the Sorax PDF page count API call due to suspicion of memleaking and heapcorrupting as per https://github.com/jimmejardine/qiqqa-open-source/issues/98 initial analysis report.

* (e353006) Code Robustness. PDFRendererFileLayer: when calculating the PDF page count happens to fail 3 times or more (Three Strikes Rule), then this PDF is flagged as irreparably obnoxious and the page count will be set to zero for the remainder of the current Qiqqa run -- this is not something we wish to persist in the metadata store as different software releases may have different page count abilities and *bugs*.

* (935a61f) Code Robustness.

* (171bf18) Performance / Code Robustness. Turning off those thread lock monitors which are hit often, take up a notable bit of CPU and are not suspect any more anyway.

* (eba4472) Fix bug where it looked like "Copy To Another Library" menu choice and "Move to Another Library" memu choice didn't differ at all: it's just that MOVE did not properly signal the sourcing library needed an update as well as the document itself.

* (1cc4d1f) Clone/Copy didn't always carry the document metadata across to the new lib. Fixed.

* (ec57707) fix crash - https://github.com/jimmejardine/qiqqa-open-source/issues/93

* (2373620) Google Analytics throws a 403. Probably did so before, but now we notice it once again as we watch for exceptions occuring in the code flow. Better logging of the 403 failure.

* (c8590be) Trying to cope with the bother of https://github.com/jimmejardine/qiqqa-open-source/issues/94 - quite a bit of it is inexplicable, unless Windows updates pulled the rug from under me (and CLR 4.0)

* (cdd51d6) Sniffer: BibTeX editor pane can toggle between formatted/parsed field editor mode and raw BibTeX editor mode.

  Known issue: the little green cross that is the UI element to toggle editor modes
  has the nauseating behaviour of moving along up & down and thus hiding behind
  the sniffer ok/fail/skip/clean buttons at top-right.

  (Pending: https://github.com/jimmejardine/qiqqa-open-source/issues/82)

* (1765137) fix https://github.com/jimmejardine/qiqqa-open-source/issues/74 + https://github.com/jimmejardine/qiqqa-open-source/issues/73 = https://github.com/GerHobbelt/qiqqa-open-source/issues/1 : QiqqaOCR is rather fruity when it comes to generating rectangle areas to OCR. This is now sanitized.

* Improved code robustness.

* Some performance improvements.

* (a3bc0b4) fix/tweak: when qiqqa server software revision XML response shows a *revert* to an older Qiqqa software release, such was coded but would not have been caught before as that bit of conditional code would never be reached when the user is running a later Qiqqa version.

* (4fd0bd1 et al) fixed 'recover desktop' functionality: screen positions and opened panes are now correctly remembered.

* (45f083d) upgrade projects to all reference .NET 4.7.2 instead of .NET 4.0 Client Profile

* (48daaa2) `support@qiqqa.com` is of course R.I.P., hence point at github issue tracker instead for software failures.

* (4f07d34) Legacy Web Library: such a library is NOT read-only. (What we got to do is point it to an 'Intranet' sync point = directory/URI path instead. (TODO)

* (bd923e5) fix https://github.com/jimmejardine/qiqqa-open-source/issues/72 + adding **minimal** support for bibtex concatenation macros in order to (somewhat) correctly parse google scholar patents records: fixes https://github.com/jimmejardine/qiqqa-open-source/issues/22 and a bit of work towards https://github.com/jimmejardine/qiqqa-open-source/issues/68

* (07bb569) allow tags to be separated by COMMA as well as SEMICOLON. (Added COMMA separator support)

* (ec1fe2c) one more for https://github.com/jimmejardine/qiqqa-open-source/issues/67

  WARNING: a PDF URI does *not* have to include a PDF extension!

  Case in point:

      https://pubs.acs.org/doi/pdf/10.1021/ed1010618?rand=zf7t0csx

  is an example of such a URI: this URI references a PDF but DOES NOT contain the string ".pdf" itself!

* (c4b64a4) PDF imports: add menu item to re-import all PDFs collected in the library in order to discover the as-yet-LOST/UNREGISTERED PDFs, which collected in the library due to previous Qiqqa crashes & user ABORT actions (https://github.com/jimmejardine/qiqqa-open-source/issues/64)

* (3872959) `AddNewDocumentToLibraryFromInternet_*()` APIs: some nasty/ill-configured servers don't produce a legal Content-Type header, or don't provide that header *at all* -- which made Qiqqa barf a hairball instead of properly attempting to import the downloaded PDF.

  Also don't yak about images which are downloaded as part of Google search pages, etc.: these content-types now make it through *part* of the PDF import code as we cannot rely on the Content-Type header being valid or present, hence we need to be very lenient about what we accept as "potentially a PDF document" to inspect before importing.

  Fixes: https://github.com/jimmejardine/qiqqa-open-source/issues/63

* (d2b5c22) tackling with the weird SQLite lockup issues: https://github.com/jimmejardine/qiqqa-open-source/issues/62

  As stated in the issue:

  Seems to be an SQLite issue: https://stackoverflow.com/questions/12532729/sqlite-keeps-the-database-locked-even-after-the-connection-is-closed gives off the same smell...

  Adding a `lock(x) {...}` critical section **per library instance** didn't make a difference.

  Adding a global/singleton  `lock(x) {...}` critical section **shared among /all/ library instances** *seems* to reduce the problem, but large PDF import tests show that the problem isn't *gone* with such a fix/tweak/hack.

* (abd020a) UPGRADE PACKAGES: log4net, SQLite, etc. -- the easy ones. Using NuGet Package Manager.

* (43debf6) remaining work for  https://github.com/jimmejardine/qiqqa-open-source/issues/56 / https://github.com/jimmejardine/qiqqa-open-source/issues/54 -- catch some nasty PDF URIs which weren't recognized as such before. Right now we're pretty aggressive as we fetch almost everything that crosses our path; once fetched we check if's actually a valid PDF file after all. CiteSeerX and other sites now deliver once again...

* (c3102a7) fix: BibTeX dialog doesn't scroll: that's a problem when your list of BibTeX tags is longer than the height of the dialog allows. Hence we can now scroll the bugger.

* (b46b38d) Don't get bothered by the Tweet stuff: collapse it.

* (e0d056c) fixes for https://github.com/jimmejardine/qiqqa-open-source/issues/56 ; also ensuring every document that's fetched off the Internet is opened in Qiqqa for review/editing (some PDF documents were silently downloaded and then dumped into the Guest Library just because and you'ld have to go around and check to see the stuff actually arrived in a library of yours. :'-(

* (be0d54f) fix: https://github.com/jimmejardine/qiqqa-open-source/issues/60 + https://github.com/jimmejardine/qiqqa-open-source/issues/39 + better fix for https://github.com/jimmejardine/qiqqa-open-source/issues/59

  check how many PDF files actually match and only move forward when we don't end up full circle. don't reflect if we didn't change. when we re-render the same document, we don't move at all!

* (4e791e8) fix https://github.com/jimmejardine/qiqqa-open-source/issues/59: don't reflect if we didn't change.

  We start with a dummy fingerprint to ensure that we will observe ANY initial setup/change as significant for otherwise we don't get the initial PDF document rendered at all!

  We use the PDF Fingerprint as a check for change as the numeric `pdf_documents_search_index` value might look easier but doesn't show us any library updates that may have happened in the meantime.

* (c8e3729) Locking in the current state of affairs as of https://github.com/jimmejardine/qiqqa-open-source/issues/55#issuecomment-524846632-permalink while I dig further to uncover the *slowtard* culprits. Mother Of All Commits. Can be split up into multiple commits if needed later on in a separate branch. Actions done in the past days while hunting the shite:

  - `FeatureTracking:GoogleAnalysicsSubmitter` begets a 403 (Forbidden) from Google Analytics. Report such in the logfile instead of letting it pass silently. (Not that I care that much about feature tracking right now, but this was part of the larger code review re HTTP access from Qiqqa)

* (c1bb4f8)
  - BibTeX Sniffer: clean up search items results in better (human readable) search criteria for some PDFs where previously the words were separated by TAB but ended up as one long concatenated string of characters in Google Scholar Search.
  - HTTP/HTTPS web grab of PDF files: we don't care which TLS/SSL protocol is required, we should just grab the PDF and not bother. Some websites require TLS2 while today I ran into a website which requires old SSL (not TLS): make sure they're **all** turned ON.
  - Register the current library with the WebBrowserHostControl so that we don't have to go through obnoxious 'Pick A Library' dialog every time we hit the "Import all PDFs available on this page" button in the browser toolbar.

* (5f00577)
  - refactor: now StandardWindow will save (and restore on demand) the window size and location for any named window; th settings will be stored in the configuration file. SHOULD be backwards compatible. Further work on https://github.com/jimmejardine/qiqqa-open-source/issues/8
  - also fix the handling of the "Has OCR" checkbox: made it a proper tri-state. VERY SLOW to filter when ticked OFF or ON. (TODO: add a hack where we only allow it to impact the filtering for N seconds so as to limit the impact on UX performance-wise)

* (720caf2)
  - fix https://github.com/jimmejardine/qiqqa-open-source/issues/54 in GoogleBibTexSnifferControl
  - Gecko these days crashes on ContentDispositionXXXX member accesses: Exception thrown: 'System.Runtime.InteropServices.COMException' in Geckofx-Core.dll

    I'm not sure why; the only change I know of is an update of MSVS2019.  :-S

  - implement the logic for the BibTeXSniffer 'Has OCR' checkbox filter criterium. It's useful but the zillion file-accesses slow the response down too much to my taste.   :-S

* (6e8ab5d) sniffer: add filter check box to only show those PDF records which have been OCRed already. (The ones that aren't are pretty hard to sniff as you cannot mark any title text bits in them yet, for instance)

* (3f1bbf2) quick fix for folder watcher going berzerk -- has to last until we refactor the async/sync PDF import code chunks. (see branch `refactoring_pdf_imports`)

* (b0b7e72)
  - 'integrate' nant build script for producing setup.exe installers into MSVS2019 solution by using a dummy project and prebuild script
  - added skeleton projects for qiqqa diagnostic and migration work. Related to https://github.com/jimmejardine/qiqqa-open-source/issues/43

* (3a2629f) working on https://github.com/jimmejardine/qiqqa-open-source/issues/52 : FolderWatcher and PDF library import need rework / refactor as we either break the status feedback to user ("Adding document N of M...") as we loose the overall count of added documents, *or* we add/import PDF documents multiple times as we cannot destroy/Clear() the list since it is fed to the async function **as a reference**. :-(

* (716d54d) fix/tweak: just like with Sniffer AutoGuess, when a BibTeX record is picked from bibtexsearch using heuristics, it is now flagged in the bibtex with a special comment (`@COMMENT...`) which was already available before in the code but apparently disused or unused until today.

* (2eb1380) refactored: Wasn't happy with the code flow in the FolderWatcher: now the long recursive directory scan (using `EnumerateFiles()`) is only aborted whn the app is terminated or when it has run its course (or when there are more or less dire circumstances); otherwise the dirtreescan is periodically paused to give the machine a bit of air to cope with the results and/or other pending work, while an app exit is very quickly discovered still (just like before, it is also detected inside the `daemon.Sleep(N)` calls in there, so we're good re that one. Tested it and works nicely. https://github.com/jimmejardine/qiqqa-open-source/issues/50

* (7118c3c) fix https://github.com/jimmejardine/qiqqa-open-source/issues/48 : Expedition: Refresh -> "Looking for new citations in ..." is not aborted when Qiqqa is closed.

* (1053fce)
  - fixed https://github.com/jimmejardine/qiqqa-open-source/issues/50 using EnumerateFiles API instead of GetFiles. (TODO: inspect other sites in code where GetFiles is invoked)
  - introduced `Utilities.Shutdownable.ShutdownableManager.Instance.IsShuttingDown` as a global flag to check whether the app is terminating: this works the same way as `!thread.IsRunning` but without the need to memoize the thread reference or pass it via extra function arguments.
  - Addd a couple of extra `IsShuttingDown` checks to improve 'exit' termination speed of the application.

* (869dea1) fixed https://github.com/jimmejardine/qiqqa-open-source/issues/8: now stores WindowState as well and fetches non-maximized window size using RestoreBounds WPF API.

* (8db7a3d) tweak the About message: now also show the *full* build version next to the classic `vNN` version.

* (7750279) make Qiqqa main app and QiqqaOCR logging easily recognizable: `[Q]` or `[OCR]` tag per logline.
  Also print the QC-reported memory usage as a fixed-width number in MBytes




# version 81.0.7158.38371 :: alpha test release
2019-08-07
----------

  * Qiqqa now copes better with damaged PDFs which are part of the librarie(s):
    + search index does not "disappear" any more
    + Qiqqa does not continue running in the background for eternity due to locked-up PDF re-indexing task

  * log outgoing activity: posting BibTeX info to bibtexsearch.com aggregator
  * re-added to 'Add This PDF to Library' button in the browser; TODO: make it work akin to the <embed> handling to prevent confusion: when the browser shows a single PDF, it MAY be an <embed> web page and we should account for that!
  * IMPORTANT FIX: this bad boy (an overzealous Dispose() which I introduced following up on the MSVS Code Analysis Reports) prevented Qiqqa from properly fetching and importing various PDFs from the Sniffer. (click on link would show the PDFs but not open them in Qiqqa nor import them into the Qiqqa library)
  * fix crash in PDF import when website/webserver does not provide a `Content-Disposable` HTTP response header
  * import PDF(s) from this web pages: added ability to cope with `<embed>` PDF links, e.g. when a HTML page is shown with PDF embedded instead of the PDF itself
  * detect PDF files in URLs which have query parameters: '.pdf' is not always the end of the URL for downloading the filename
  * added CHANGELOG (partly edited & full version using git log)
  * Whoops. Crash when quickly opening + closing + opening.... Sniffer windows: CLOSE != DISPOSE. Crash due to loss of search_options binding on second opening...
  * Only when you play with it, you discover what works. The HasSourceURL/Local/Unsourced choices should be OR-ed together as that feels intuitive, while we also want to see 'sans PDF' entries as we can use the Sniffer to dig up the PDF on the IntarWebz if we're lucky. Meanwhile, 'invert' should clearly be positioned off to a corner to signify its purpose: inverting your selection set (while it should **probably** :thinking: have no effect if a specific document was specified by the user: then we're looking at a particular item PLUS maybe some other stuff?
  * Sniffer Features:
    - add checkboxes to (sub)select documents which have a URL source registered with them or no source registered at all. (https://github.com/jimmejardine/qiqqa-open-source/issues/29)
    - add 'invert' logic for the library filter (https://github.com/jimmejardine/qiqqa-open-source/issues/30)
  * fix https://github.com/jimmejardine/qiqqa-open-source/issues/28: turns out Qiqqa is feeding all the empty records to the PubMed-to-BibTex converter, which is throwing a tantrum. Improved checks and balances and all that. Jolly good, carry on, chaps. :-)
  * report complete build version in logging.
  * improving the logging while we hunt for the elusive Fail Creatures...
  * Code Quality / Stability work following up on Microsoft Visual Studio Code Analysis Reports et al.
  * done work on https://github.com/jimmejardine/qiqqa-open-source/issues/27 and on the lockups of Qiqqa (some critical sections in there were **humongous** in both code side and run-time duration; now the number of lock-ups due to *very* slow loading PDFs coming in from the Qiqqa Sniffer should be quite reduced: work related to https://github.com/jimmejardine/qiqqa-open-source/issues/18

2019-08-07
----------

  * fix crash when quickly opening + closing + opening.... Sniffer windows

  * Sniffer Features:

    - add checkboxes to (sub)select documents which have a URL source registered with them or no source registered at all. (https://github.com/jimmejardine/qiqqa-open-source/issues/29)

      Note: Only when you play with it, you discover what works. The HasSourceURL/Local/Unsourced choices are OR-ed together as that feels intuitive, while we also want to see 'sans PDF' entries as we can use the Sniffer to dig up the PDF on the IntarWebz if we're lucky. Meanwhile, 'invert' is positioned off to a corner to signify its purpose: inverting your selection set (while it should **probably** :thinking: have no effect if a specific document was specified by the user: then we're looking at a particular item PLUS maybe some other stuff?)

     - add 'invert' logic for the library filter (https://github.com/jimmejardine/qiqqa-open-source/issues/30)

  * fix https://github.com/jimmejardine/qiqqa-open-source/issues/28: turns out Qiqqa is feeding all the empty records to the PubMed-to-BibTex converter, which is throwing a tantrum. Improved checks and balances and all that. Jolly good, carry on, chaps. :-)

  * report complete build version in logging.
  * improving the logging while we hunt for the elusive Fail Creatures...
  * Code Quality / Stability work following up on Microsoft Visual Studio Code Analysis Reports et al.

2019-08-06
----------

  * using a more Microsoft-like build versioning approach. 81.x.y.z where y.z is a build ID

  * feature added: store the source URL (!yay!) of any grabbed/sniffed PDF. Previously the source path of locally imported (via WatchFolder) PDFs was memorized in the Qiqqa database. It adds great value (to me at least) when Qiqqa can also store the source URL for any document -- this is very handy information to have as part of augmented document references!)

  * Code Quality / Stability work following up on Microsoft Visual Studio Code Analysis Reports et al.



2019-08-05
----------

  * Don't let illegal multiple BibTeX entries for a single PDF record slip through unnoticed: one PDF having multiple BibTeX records should be noticed as a WARNING at least in the logging.
  * some invalid BibTeX was crashing the Lucene indexer (AddDocumentMetadata_BibTex() would b0rk on a NULL Key)
    Sample invalid BibTeX:
        @empty = delete?
  * trying to tackle the slow memory leak that's happening while Qiqqa is running  :-((
  * DBExplorer severely enhanced:
    - now supports wildcards in query parameters (% and _, but also * and ?, which are the MSDOS wildcards which translate directly to the SQL wildcards)
    - now supports GETting multiple records.
    - when GETting multiple records, DBExplorer not only prints the BibTeX for each record, but also the identifying fingerprint, verification MD5 and most importantly: the *PARSED* BibTeX (iff available) and BibTeX parse error diagnostics report.
    - when GETting multiple records, the DBExplorer output is also dumped to the file Qiqqa.DBexplorer.QueryDump.txt in the Qiqqa Library base directory. A previous DBExplorer query report dump will be REPLACED.
    - an extra input field has been added which allows the user to specify a maximum number of records to fetch: this speeds up queries and their reporting when working on large libraries with query criterai which would produce 1000nds of records if left unchecked.
    This allows to use the DBExplorer as a rough diagnostics tool to check the library internals, including a way to find erroneous/offending BibTeX entries which may cause havoc in Qiqqa elsewhere.

2019-08-04
----------

  * fixing https://github.com/jimmejardine/qiqqa-open-source/issues/8: not only storing Left/Top coordinate, but also Width+Height of the Qiqqa.exe window
  * fix crash in chat code when Qiqqa is shutting down
  * Since ExpeditionManager is the biggest OutOfMemory troublemaker (when loading a saved session :-( ), we're augmenting the logging a tad to ease diagnosis. (https://github.com/jimmejardine/qiqqa-open-source/issues/19)
  * debugging: uncollapsing rollups in dialog windows as part of a longer debugging activity. MUST REVERT!
  * 'Open New Browser' was looking pretty weird due to a website/page being loaded which was unresponsive; now we're pointing to a more readily available webpage instead. (Though in my opinion 'Open Browser' should load a VERY MINIMAL webpage, which has absolutely *minimal* content...)
  * Mention the new CSL (Citation Styles) source websites in the credits.
  * code stability: Do not crash/fail when the historical progress file is damaged

2019-08-03
----------

  * The easy bit of https://github.com/jimmejardine/qiqqa-open-source/issues/3: synced the Qiqqa/InCite/styles/ directory with the bleeding edge of the CSL repo at https://github.com/citation-style-language/styles (Note the 'bleeding edge' in there: I didn't use https://github.com/citation-style-language/styles-distribution !). DO NOTE that Qiqqa had several CSL style definitions which don't exist in this repository: these have been kept as-is.

2019-08-02
----------

  * tackling spurious application lockups and extremely unresponsive behaviours. Addresses these issues:
    + https://github.com/jimmejardine/qiqqa-open-source/issues/18
    + https://github.com/jimmejardine/qiqqa-open-source/issues/17
    + https://github.com/jimmejardine/qiqqa-open-source/issues/10
    + https://github.com/jimmejardine/qiqqa-open-source/issues/20

  * Fix https://github.com/jimmejardine/qiqqa-open-source/issues/17 by processing PDFs in any Qiqqa library in *small* batches so that Qiqqa is not unreponsive for a loooooooooooooong time when it is re-indexing/upgrading/whatever a *large* library, e.g. 20K+ PDF files. The key here is to make the '**infrequent background task**' produce *some* result quickly (like a working, yet incomplete, Lucene search index DB!) and then *updating*/*augmenting* that result as time goes by. This way, we can recover a search index for larger Qiqqa libraries!

  * dialing up the debug/info logging to help me find the most annoying bugs, first of them: https://github.com/jimmejardine/qiqqa-open-source/issues/10, then https://github.com/jimmejardine/qiqqa-open-source/issues/13

  * Do NOT nuke the previous run's `Qiqqa.log` file in `C:\Users\<YourName>\AppData\Local\Quantisle\Qiqqa\Logs\`: **quick hack** to add a timestamp to the qiqqa log file so we'll be quickly able to inspect logs from multiple sessions.

    **Warning**: this MUST NOT be present in any future production version or you'll kill users by log file collection buildup on the install drive!

  * simple stuff: updating copyright notices from 2016 to 2019.

  * update existing Syncfusion files from v14 to v17, which helps resolve https://github.com/jimmejardine/qiqqa-open-source/issues/11

    **Warning**: I got those files by copying a Syncfusion install directory into qiqqa::/libs/ and overwriting existing files. v17 has a few more files, but those seem not to be required/used by Qiqqa, as **only overwriting what was already there** in the **Qiqqa** install directory seems to deliver a working Qiqqa tool. :phew:

  * updating 7zip to latest release

Version 80 (FOSS):
=================


> ## Note
>
> This release is **binary compatible with v80 and v79**: any library created using this version MUST be readable and usable by v80 and v79 software releases.





- Qiqqa goes Open Source!!!
- Enabled ALL Premium and Premium+ features for everyone.
- Removed all Web Library capabilities (create/sync/manage)
- Added the ability to copy the entire contents of a former Web Library into a library - as a migration path from Qiqqa v79 to v80




----

**Start of the Qiqqa Open Source activity**

----





Commercial Qiqqa releases
=========================


Version 79 (Commercial):
- Can add regularly used user-defined keys to the BibTeX Editor
- Can add regularly used search queries to the Search Boxes.
- Adds Jamatto donate buttons to the PDF Share feature.
- Check out Qiqqa for Web at http://web.qiqqa.com

Version 78:
- Bundle Libraries allow you to bundle up libraries for read-only dstribution of your content to your customers.
- Can export linked-documents data.
- Custom abbreviations can override default ones.
- Font size change in Speed Reader.
- Fixes a BibTeX parse error causing problems with Qiqqa starting.

Version 77:
- You can override the location of your PDF and OCR files.

Version 76:
- Improved BibTeX Sniffer where you can scan linearly and review automatically found BibTeXes.
- Improved InCite screen.
- Improved location of highlighter, annotation tools in PDF Reader.

Version 75:
- Can attach PDFs to Vanilla References using Web Browser.
- Can toggle BibTeX Search Wizard and Automatic BibTeX association.
- Automatically import from EndNote.
- Qiqqa Community Chat.
- Latest embedded Firefox browser.
- Locked PDFs do not cause the Annotation Report to stop halfway through.

Version 74:
- Can watch multiple folders.
- Can automatically attach tags to PDFs from watched folders.
- Can export tags, autotags, etc.
- Updated lucene library to fix corrupted search index on rare occasions.
- Moves to the top of the library after sorting.

Version 73:
- Friendlier configuration screen.
- Scrolls to the top of the document list when a filter or sort changes.
- Annotation Report: Removes menu hyperlinks from annotation report on export to Word; Abstract and Comment titles.
- PDF renderer is robust to a variety of corrupted PDF types.
- PDFs are not blurry on *all* LCD monitor types
- If necessary, Qiqqa can now use up to 4Gb RAM on 64-bit machines.  No longer limited to circa 1.2Gb.

Version 72:
- Qiqqa automatically associates BibTeX with well-known PDFs.
- Public status web libraries
- Better duplicates detector.
- Improved brainstorm auto layout
- Can tweet a document from the document reader
- Can get a username reminder from login screen.
- Batches PDF uploads so that massive libraries (e.g. 20,000+ docs) do not time out on slow networks.
- Fix to brainstorm resize exception

Version 71:
- Can link documents so that you can quickly jump between them.
- Can customise library icon and background.
- Can open a PDF from the BibTeX Sniffer.
- Qiqqa's proxy support now includes using your Windows-user or network-user details.
- Can add 1000s of documents more quickly.
- OCR automatically uses all but one of your CPUs
- Can locate an Intranet sync folder location.

Version 70:
- Downloads of upgrades are MUCH faster.
- Premium Web Library storage space is increased to 10Gb, free storage space to 2Gb!
- Smoother highlighting.
- Library search always causes the sort mode to switch to Search Score.
- Explanation of recommendations on Start Page.
- Can resize Annotations on a PDF by double tapping and dragging - great for tablets.
- Can right-click and add an AutoTag to the while- or blacklists.
- Can promote an AutoTag to a Tag.
- Can explore an AutoTag in a Brainstorm.
- Automatically detects when you sync from another computer and syncs immediately.
- Autodetects new library memberships and new premium payments.
- Fixed the 'forgotten watch folder when you refresh memberships' issue.
- Authors in BibTeX are now split on 'mixed case aNd'

Version 69:
- You can filter annotation in the Annotation Report by creator.
- Improvements to Annotation Report formatting.
- "BibTeX Type" library filter.
- Welcome Wizard gets you up to speed with Qiqqa quickly.
- Mass-download all PDFs in web browser handles more types of URL and content type.
- Web Browser status messages.
- Ctrl-F jumps to search box.

Version 68:
- Supports imports of patent portfolios from Omnipatents.
- Can mass-download all PDFs linked to by a web page.
- Open PDF tabs are coloured.

Version 67:
- Novice/Expert mode.
- Mass edit documents metadata.
- Customised Reading Stages.
- Pivot Table of library statistics.
- Share Annotations and Brainstorms via Social Media.
- Redesigned Qiqqa InCite screen.
- Improvement to 'blue book' citation snippet formatting.
- Miscellaneous changes to GUI to remove clutter.
- Fixed window redock exception.

Version 66:
- Can filter annotations by date in the Annotation Report.
- Can add prefixes and suffixes to InCite citations.
- Sort has moved to filter area for better screen use.
- Page number in PDF Reader now respects start page number in BibTeX
- Improved citation editor control.
- Improved annotation editor control.
- Vastly improved title recognition for better BibTeX Sniffer results.
- Can move PDFs between libraries.
- EZProxy support.
- Can toggle appearance of SpeedRead shadow text.
- Improved printing of Brainstorms.
- Fixed the 'bug' where a new PDF in the watch folder 'steals' the currently selected focus.
- Much faster addition of 1,000s of PDFs.

Version 65:
- Share PDF annotations via social media.
- Sort tags, authors, etc. in the library filter by frequency.
- Web page HTML to PDF conversion is now completely inside Qiqqa, so it is more stable and has better features.
- Further integration with Datacopia.com to automatically create beautiful charts from tables of results.
- Improved stability for import where Mendeley points to broken files.

Version 64:
- BibTeX Sniffer supports international characters
- Libraries open much more quickly - especially libraries with more than 10k+ documents.
- Importing PDFs is much faster.
- Batch importing of PDFs no longer aborts after the first missing PDF: instead a report of errors is offered at the end of the import.
- Now supports 'ridiculously long filenames'.
- Updated the bundled Firefox browser to latest version - improves stability of internal web browser.

Version 63:
- Integration with Datacopia.com to automatically create charts from tables of results.
- *SpeedRead* your way through PDFs at up to 1000 WPM.  Awesome!
- Massive improvements to brainstorm for PDF document nodes and their annotations.

Version 62:
- Integration with Datacopia.com to automatically create charts from tables of results.
- Support for Bundle Libraries.
- Better author name disambiguation
- Vastly improved brainstorm automatic layout algorithm
- Thumbnail PDF pages
- Jump to the library containing a PDF

Version 61:
- You can automatically create a BibTeX record from the suggested metadata.
- Pressing CTRL-; in the BibTeX editor will add the current date (useful for the accessed field of a website record).
- Better instructions on how to cancel a Watch Folder.
- Improvements to the Import feature.

Version 60:
- When you now explore Documents or Themes in a brainstorm (right click and explore), you get some pretty epic pictures of your library.
- The BibTeX editor now offers the legal-case type.
- InCite now has separate toolbar buttons for citing (Author, Year) and Author (Year).
- PDF pages are now centered in the reader.
- The Qiqqa InCite popup can now also be activated using Win-A as well as Win-Q.

Version 59:
- You can sync to Intranet libraries even when not connected to the Internet.
- You can rotate all pages at once.
- Patch: Fixes the sync problem if you don't have a proxy.

Version 58:
- German and Turkish translations.
- Patch: InCite maps the "article" type to CSL "article-journal" so that journal and page numbers are included in the bibliography.

Version 57:
- Search queries are remembered.
- Can log in with default network proxy credentials.
- 50Gb Web Libraries for Premium+ members.
- Annotation report is ordered according to Library Screen.
- All CSL document types and location types are supported.
- Highlight rendering speed dramatically improved for long documents.

Version 56:
- Documents can have colours associated with them.
- Document title and size is coloured and sized accouring to reading stage and rating.
- Fixes Word connectivity on computers where Word has been incorrectly installed and uninstalled.
- All Document metadata is visible at once on tall screens.
- Can mass-rename publications
- F11 goes full-screen while reading PDFs
- Fixed a memory leak while reading large PDFs.

Version 55:
- Premium Fields allow you to restrict your searches to ANY of the fields that you have added in your PDF BibTeX records.
- Qiqqa now supports the Bluebook legal CSL style.
- Qiqqa supports the "short form" of journal name in your bibliographies.
- You can refresh the Annotation Report for a PDF or jump straight to a full blown Annotation Report.
- Qiqqa warns about DropBox conflicts.

Version 54:
- Added the Qiqqa Manual.

Version 53:
- Compatibility with Word 2013.
- Drag and drop PDFs straight onto Start Page libraries.
- Can export Expedition themes to text.
- Can sort PDFs by page count.
- The BibTeX types incollection inproceedings inbook chapter all map to CSL chapter type

Version 52:
- Qiqqa Champion Project.
- Support for online CSL editor.
- Individually control highlight, annotation and ink transparencies.
- Better feedback from InCite when you have a problematic reference.
- Library export has an HTML summary.
- Annotation reports are not automatic if they are too large.
- Can rebuild indices corrupted by DropBox, GoogleDrive, etc.

Version 51:
- Automatic PubMed support in BibTeX Sniffer.
- OCR supports several European languages.
- Adding a non-PDF reference automatically popup up the BibTeX editor.
- Favourites now show up with hearts in library view.
- Can explore libraries in brainstorm.
- InCite is much faster at updating references in Word.
- BibTeX Sniffer editor window is resizable.
- Better keyboard shortcut handling.
- Better zoom behaviour.

Version 50:
- Umbrella-search across all your libraries.
- Can expand most INFLUENTIAL and most SIMILAR papers for a theme in brainstorm.
- Smarter BibTeX Sniffer that highlights author names for fast cross-check.
- Smarter BibTeX Sniffer Wizard.
- Tag filters now have checkboxes for more intuitive multi-select.
- PDF preview popup has Expedition Themes.
- Can copy BibTeX key from PDF Reader screen.
- Can sort library by whether or not a document has associated BibTeX.
- You can now choose between using Tags, AutoTags or both when building your Expedition.
- "CSV database" of metadata added to Library Export.

Version 49:
- Supports read-only Web Libraries.
- Supports read-only Intranet Libraries for Premium members.
- Can import legacy PDF annotations and highlights.
- Qiqqa remembers screen location at shutdown.

Version 48:
- Libraries can be filtered by Expedition theme.
- The filter graph shows more columns.
- You can create Web Libraries from within the Qiqqa Client.
- Stability:
  + Fixes more issues around Firefox DLL clashes.

Version 47:
- Remembers last page N-up settings.
- Deleted PDFs no longer appear in cross references.
- Stability:
  + Fixes issues with clients with non-standard DPI display settings (highlighting positions do not match text).
  + Fixes issues with PDFs with corrupted XRef tables.
  + Fixes some issues around Firefox DLL clashes.

Version 46:
- Win+Q key combination brings up a mini-InCite screen so that you can easily add citations to Word.
- Expedition theme colours are visible throughout Qiqqa.
- You can print from the Browser.
- Performance improvements to the PDF renderer and to startup time.

Version 45:
- Qiqqa Premium+
- Qiqqa now supports Intranet Libraries, where you can sync completely internally to your corporate intranet.
- Automatically convert Microsoft Word files to PDF.
- You can delete duplicates in the duplicate detection screen.
- Brainstorms can automatically neaten themselves.

Version 44:
- The built-in browser uses Firefox, not Internet Explorer.
- Browsing a PDF document in the built-in web browser will automatically add it to your Guest library and offer for you to move it.
- Can turn on automatic synchronisation, so you never have to worry about forgetting to sync before leaving the office.
- Can add InCite fields to floating text areas too.
- InCite fields are locked in Word by default so that you don't need Qiqqa on a computer to maintain the contents of the fields.
- Can run a report to see which documents you have cited in InCite.
- Can open a document just by moving the mouse cursor over it in Word and pressing ENTER in Qiqqa InCite.
- BibTeX abstracts are shown in abstract sidebar when present.
- Uploads of large PDFs work over slow connections.
- You can cite Author (date) and (Author, Date) from the PDF library and PDF reader menus.
- Better duplicate detection with sort.
- Clearer PDF rendering.
- Improved keyword cloud using autotags.
- Massive all-round speed enhancements - now tested with libraries of up to 15,000 documents.

Version 43:
- NB: THIS VERSION REQUIRES AN AUTOMATIC UPGRADE TO MICROSOFT'S .NET4 FRAMEWORK if you are running an earlier version of Qiqqa than v40.
- NB: So only update if you have about 30 minutes and no urgent project deadlines.
- You can now see all duplicates across your library.
- Highlight/select/ink tools are below the toolbar items.

Version 42:
- NB: THIS VERSION REQUIRES AN AUTOMATIC UPGRADE TO MICROSOFT'S .NET4 FRAMEWORK if you are running an earlier version of Qiqqa than v40.
- NB: So only update if you have about 30 minutes and no urgent project deadlines.
- The start page now shows the coverpages of your recommended reading.
- You can turn off secure SSL communication with the Qiqqa Cloud.
- Qiqqa warns you if you cite a document that has a duplicate or a blank BibTeX key.
- Qiqqa now remembers which libraries and documents you last had open.
- Can purge deleted files from the config screen.

Version 41:
- NB: THIS VERSION REQUIRES AN AUTOMATIC UPGRADE TO MICROSOFT'S .NET4 FRAMEWORK.
- NB: So only update if you have about 30 minutes and no urgent project deadlines.
- Can cite documents from pdf reader and annotation report.
- Added "id" field to library catalog.
- Prettier library catalog layout.
- Fixed delayed update in BibTeX editor.
- Tidier menu bars.

Version 40:
- More brainstorm features - group select, better node represenations.
- Library export adds file and filename fields to BibTeX.

Version 39:
- Menus in French, German, Mandarin Chinese, Polish, Portuguese & Taiwanese.
- Qiqqa now supports password-protected PDFs.
- 8Gb storage for Premium Members.
- "Webpage" InCite and BibTeX type.
- Better highlight extraction in annotation reports.
- Performance improvements - at startup, when generating AutoTags and when generating Annotation reports.

Version 38:
- NB: This version will require an update to your Qiqqa database,
- NB: so although we have heavily tested this release,
- NB: be prudent and don't upgrade if you have a looming hard paper deadline... :-)
- You can associate PDFs with Vanilla References.
- Right-click copy BibTeX keys for fast pasting into LaTeX.
- Speed improvements at startup and during sync.
- Fixed the InCite SURNAME p. (DATE p.) issue.

Version 37:
- Built-in CSL style editor.
- You can now look inside your library search results without having to open each PDF.
- You can now contribute to the translation of Qiqqa into your own language.
- Expedition details in PDF Reading screen.
- Speed improvements to OCR.

Version 36:
- Qiqqa Expedition - Qiqqa helps you understand your research literature landscape.
- Ink annotations now show up in Annotation Report.
- Can include abstracts in Annotation Report.
- Brainstorm support multiline text.
- Open PDF multiple times.
- Improved highlighting mode.
- New webcasts for Brainstorms and Expedition.

Version 35:
- Premium Membership get you 1Gb of free Web Library space.
- Themed colours for Qiqqa.
- Qiqqa help forums.
- New Qiqqa features webcast.

Version 34:
- Awesome annotations summaries in side-bars.
- Better search results.
- Can reverse your sorts with 2nd click.
- Paper abstracts are automatically extracted.
- A great new introductory webcast by the McKillop Library.
- InCite tidies up spurious spaces around citations.

Version 33:
- Support for Qiqqa for Android!  Please make sure you upgrade to at least Qiqqa v31 on ALL your computers...
- DON'T UPGRADE IF YOU HAVE A DEADLINE THIS WEEK - just in case! :-)
- Last reading page and bookmarks are remembered.
- You can filter to PDFs that have no tags at all.

Version 32:
- Share and email a document
- Faster opening of PDFs

Version 31:
- Can backup to ZIP file.
- Better BibTeX Sniffer wizard.
- Improved EndNote importing.
- Improvements to Start Page.
- Additional webcasts and helper tips.
- Better folder watching.

Version 30:
- Qiqqa InCite - copy single citation snippets to the clipboard for pasting into OpenOffice and emails.
- More powerful search result ranking by relevance.
- Duplicate detection with indicator warning.
- Bookmarks while reading your PDFs so you can jump back-and-forth to the bibliography.

Version 29:
- Qiqqa InCite released - including dependent CSL styles.
- More powerful library search facility with quoted, boolean, proximity, fuzzy and field searches.
- WARNING: Will automatically rebuild your document indices, so please be patient for a few minutes.

Version 28:
- Faster PDF text extract and index
- You can force OCR on pages where the embedded text is corrupt in the PDF.
- Qiqqa Library export to directory.

Version 27:
- Qiqqa InCite BETA improvements (more styles, Word XP support, error messages).
- Webcasts introducing and demonstrating some of the Qiqqa functionality.

Version 26:
- Qiqqa InCite, Qiqqa's Microsoft Word bibliography management system.
- Web proxy support.

Version 25:
- Full screen reading mode.
- Recommended reading on Start Page.

Version 24:
- Full BibTeX editor.
- Better document metadata editors.
- Document metadata editors available from document library.
- Speed improvements.

Version 23:
- Explore your documents using brainstorms.
- Better BibTeX sniffer.
- Multicoloured text highlighting.
- Printing now contains your annotations and highlights.
- Better PDF text clarity.
- More EndNote article export types.
- Qiqqa Premium features.

Version 22:
- Improved tablet support.
- Performance and other minor enhancements.
- WARNING: Will automatically rebuild your document indices, so please be patient.

Version 21:
- Unlimited libraries.
- Sharper PDF rendering.
- Cross references for your papers.
- Improvements to the BibTeX sniffer.

Version 20:
- A lot of new PDF search functionality.
- Can copy and delete multiple PDFs in the library catalog.

Version 19:
- Import from EndNote, Zotero, Mendeley.
- Import PDFs recursively from folders and tag them with their folder names.
- Ink annotations for tablets.

Version 18:
- The first installer version of Qiqqa available for beta testing!

