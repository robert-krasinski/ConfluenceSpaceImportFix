Script for fixing following issue when importing Confluence space:

Error during import Confluence space from another instance:
com.atlassian.confluence.importexport.ImportExportException:
Unable to complete import: Error while importing backup: org.hibernate.exception.ConstraintViolationException:
could not execute statement

https://jira.atlassian.com/browse/CONFCLOUD-45278
Can you please check and confirm if your space import is failing because of this particular issue,
by following the next steps:

Extract your space export archive.

Open the entities.xml file in a text editor.

Search for the following pattern:
<object class="Space" package="com.atlassian.confluence.spaces">
If more than 1 result is returned, you will need to remove the additional space declarations
(look at the space key or space name to confirm which ones you need to remove).
When removing the additional entries, make sure to remove everything between the opening
<object class="Space" package="com.atlassian.confluence.spaces"> and its closing tag </object> (object tags included).
Rezip your space export archive and make sure that both entities.xml and exportDescriptor.properties files
are located at the root of your archive.
  
Check the Space permissions menu in your instance Confluence administration and remove the corrupted space
(result of the failed import).

Attempt a new space import with the fixed archive.


Notes for OS X users
If you perform this action on Mac OS X, hidden files may be included in the archive after you compress it.
You will need to open the Terminal, go to the folder where the archive is located and clean it using
the following commands:

zip -d ArchiveName.zip __MACOSX/\*
zip -d ArchiveName.zip \*/.DS_Store
