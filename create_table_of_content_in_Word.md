# Create Table of Content or Appendix in Word for Mac

This guide works well for the following environmental parameters:

- Microsoft Word for Mac, Version 16.16.14
- macOS Mojave, Version 10.14.6

Creating a table of content or appendix in Word is not as intuitive as you might think. 

In a Word document, first we create the sections that shall be indexed into an appendix. In a blank page, type a dummy section title such as `Appendix A: who are we`, insert a page break behind this tile with `Insert/Break/Page Break`. Inserting a page break is not a must-have, but it makes the doc look cleaner and more professional. 

Use cursor to full-select this section title, then `Format/Style/` to open up the dialog window of selecting styles. Microsoft does a phenomenal job of confusing users here with no explanation or guidance on which styles are applicable for the purpose of creating a TOC or appendix. Index 1-9, TOC 1-9, Heading 1-9, all seem to be fair game. 

The most important tip here is to select `Heading 1-9`. This is the set of styles are are linked to TOC/appendix by a mysterious force of nature embedded in Microsoft's comprehensive product design logic. Index 1-9, TOC 1-9 will NOT work. 

I would go with `Heading 1`. Apply the same style on every section title. 

Move the cursor to the beginning of the TOC/appendix area (before every appendix section title obviously), go `References/Table of Contents/` and select a TOC style. I use `Formal`. 

Magically, a self-populated section behind the cursor appears, with a nicely formatted Table of Contents (Appendix). Voila!

Right click on this TOC section, and `Update Field` to update this TOC with additional section titles or page numbers. 

At this point, a skeleton structure of TOC/appendix has been created. You can go ahead to fill up each section with actual text, charts and diagrams. In essence, the trick is to format section titles with one uniform style, and make sure Table of Contents auto-text can pick up that particular style and self-populate and auto-update with page numbers. 

***

[Back to HitichHikder's Guide by Herbert](README.md)