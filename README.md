# mediawiki-extensions-SemanticACL
Github mirror of MediaWiki extension SemanticACL - our actual code is hosted with Gerrit (please see https://www.mediawiki.org/wiki/Developer_access for contributing)

# Default policy 'only users'
WARNING: Untested feature!

SemanticACL is well suited to prevent access explicitly, e. g. only for logged-in user in a public wiki or only user of a specific group in a private wiki.
It's not possible to allow explicit access to a page, e. g. for anon users in a private wiki.

This branch patches SemanticACL to enable this feature. 
Therefore the wiki has to be set to 'pseudo public', meaning 

`$wgGroupPermissions['*']['read'] = true;`

in LocalSettings.php, but SemanticACL limits access instead of the core mediawiki by disables access for anon users any on pages without any SemanticACL Properties (exempt pages whitelistet with `$wgWhitelistRead[]`) 

Because img_auth.php evaluates `$wgGroupPermissions['*']['read']`, this file has to be patched as well by replacing 

`$publicWiki = in_array( 'read', User::getGroupPermissions( [ '*' ] ), true );`

with

`$publicWiki = false;`
