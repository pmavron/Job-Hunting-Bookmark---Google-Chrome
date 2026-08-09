# Job-Hunting-Bookmark---Google-Chrome
Over 1500 links to links to 1500+ NYSE companies.
* Select 3 dots top-right on chrome browser > bookmarks and list > Import bookmarks and settings > Select bookmarks html file > upload companies.html
* Your bookmarks folder will appear at the bottom of your bookmarks tab.

You can also generate your own html file in: Excel > Appscript

Template Code:

function exportToChromeBookmarks() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = sheet.getDataRange().getValues();
  
  var html = '<!DOCTYPE NETSCAPE-Bookmark-file-1>\n' +
             '<META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=UTF-8">\n' +
             '<TITLE>Bookmarks</TITLE>\n' +
             '<H1>Bookmarks</H1>\n' +
             '<DL><p>\n' +
             '    <DT><H3>Sheet Bookmarks</H3>\n' +
             '    <DL><p>\n';
  
  for (var i = 1; i < data.length; i++) {
    var title = data[i][0]; // Column A (Company Name)
    
    if (title && title.toString().trim() !== "") {
      var cleanTitle = title.toString().trim();
      // Dynamically construct the Google Search URL for Chrome Bookmarks
      var searchUrl = "https://www.google.com/search?q=" + encodeURIComponent(cleanTitle + " careers");
      
      html += '        <DT><A HREF="' + searchUrl + '">' + cleanTitle + ' Careers</A>\n';
    }
  }
  
  html += '    </DL><p>\n</DL><p>';
  
  DriveApp.createFile('companies.html', html, MimeType.HTML);
  Logger.log('Saved to Google Drive as companies.html');
}
