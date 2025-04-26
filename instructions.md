# **my endless-sky-plugins**

## instructions

<ul>
  <li>upload this plugin repo template to your new github repository. be aware of hidden folders and files and get sure all of them are uploaded.</li>
  <li>go to the repo settings: actions>general: activate 'Allow all actions and reusable workflows'</li>
  <li>go to the repo settings: actions>general: workflow permissions: activate 'Read and write permissions' </li>
  <li>.github/workflows/(manual) create release.yml: change 'git config user.name "zuckung"' to your username</li>
  <li>.github/workflows/(manual) create release.yml: change 'git config user.email "zuckung@gmx.de"' to your email</li>
  <li>.github/workflows/(manual) make md.yml: change 'git config user.name "zuckung"' to your username</li>
  <li>.github/workflows/(manual) make md.yml: change 'git config user.email "zuckung@gmx.de"' to your email</li>
  <li>delete myplugins/example.plugin/ and put your plugins into the myplugins folder. the plugin needs an icon.png, an about.txt, a data folder(with content), and its own README.md, so the repo README can get generated out of these data. name your plugin without spaces or special characters. use dots or no spaces(i.e. example.plugin, ExamplePlugin). that is because when releasing, github replaces special characters or spaces with a dot. if you don't use this naming convention the links might be wrong.</li>
  <li>run '(manual) create release' workflow from the actions tab, type in the exact name of the plugin, and wait a minute. the release got created and a new README.md got written.</li>
  <li>you are done. read the rest of this instructions to see how the files system works and what else you can do.</li>
</ul>

## details for folders and files

.github/workflows/(manual) create release.yml
<ul>
  <li>this is the workflow you use for releasing a plugin. after plugin upload, go to action tab, click the workflow, click run workflow, enter the exact plugin name(else it fails) and let it run(it takes a minute to finish). it puts outs a release with an asset zip and with an increasing version number, noted in /res/versioning.txt. this workflow also generates the readme.md taking in all plugins, screenshots, the newly generated asset zip and other data. so never edit the readme, it gets overwritten on release.</li>
</ul>    
    
.github/workflows/(manual) make md.yml
<ul>
  <li>this workflow is also run manually in case you want to change the readme without pushing a release. it does the same as the previous workflow just without the release. the readme content (beside the variable content, like plugins, paths etc) is read out of res/template.txt</li>
</ul>

.github/workflows/(on push) spellcheck.yml
<ul>
  <li>this workflow runs on every push and checks for spelling errors inside the whole repositor. it fails if an error is found and shows where it is.</li>
  <li>.codespell.exclude and .codespell.words.exclude can be edited to whitelist words, currently filled with my excludes as an example.</li>
</ul>

.github/workflows/(on push) data check.yml
<ul>
  <li>this workflow runs on every push and checks for ES script errors inside the myplugins folder. it fails if an error is found and shows where it is.</li>
  <li>that is done by starting the game on the github server, loading the plugins and reporting the errors.</li>
</ul>

myplugins/example.plugin
<ul>
  <li>an example plugin to show you how it should look.</li>
</ul>

res/template.txt
<ul>
  <li>from here comes the static readme.md content. this textfile is splitted into 2 part, the upper static content,  and the variable plugin template, separated by %plugin template below this line%'. each plugin gets this plugin template written to the README. it works with variables like '%variablename%'. these get replaced on generation. both parts can be mixed in html and markdown. experiment. i.e '%description%' variable gets replaced by the content from about.txt, '%size%' by kb/mb size, '%readme%' by the plugin readme.md content etc.</li>
<li>useable variables inside template.txt:<br>
%news%           html table of the latest 10 news entries<br>
%pluginlist%     html table of anchor links to all plugins<br>
%name%           the plugin name<br>
%icon%           html img with plugin icon url, i.e <code>&ltimg src="myplugins/PluginName/icon.png" height="100"&gt</code><br>
%assetfile%      release zip name of the plugin, special chars and spaces are replaced by dots, i.e <code>PluginName.zip</code><br>
%assetfullpath%  url to the plugin release, i.e. <code>https://github.com/YourUserName/YourRepoName/releases/download/v1.0.1-PluginName/</code><br>
%size%           plugin size in mb or kb, or 'N/A' if no release found, i.e. <code>245.07 kb</code><br>
%lastmodified%   last modified date of the plugin release zip file, or 'N/A' if no release found, i.e <code>2025-04-17</code><br>
%pluginurl%      url path to the plugin folder, i.e. <code>https://github.com/YourUserName/YourRepoName/tree/main/myplugins/</code><br>
%pluginnameurl%  plugin folder name, with space replaced by %20, i.e. <code>PluginName</code><br>
%imagemd%        html link to a seperate plugin md file with all images of that plugin, i.e. <code>&lta href="res/imagemd/PluginName.md"&gtview images&lt/a&gt [47]</code><br>
%description%    content of the plugin's' plugin.txt's about or of about.txt, or <code>N/A</code> if none found<br>
%readme%         content of the plugin's' README.md or <code>N/A</code> if none found<br>
%screenshots%    html table of the plugin screenshots from the screenshot folder, or '' if none found<br>
%version%        version number, i.e. <code>1.1.12</code></li>
</ul>

res/news.txt
<ul>
  <li>when releasing a plugin a new entry is made automatically, but manual entries work too. to change something just edit this file and on next readme generation workflow the newsbox is updated. the last 10 news entries are shown in the plugin template with the %news% variable.</li>
</ul>

res/versioning.txt
<ul>
  <li>if the plugin version isn't in this textfile it gets written to it and set to version '1.0.0'. with every run it increases by '0.0.1'. manually changing works. i.e. setting version to '1.1.0' or' 2.4.0' in versioning.txt.</li>
</ul>

res/src
<ul>
  <li>python files. no need to touch them. the news box or the plugin variables get their content structure from here.</li>
</ul>

res/imagemd/
<ul>
  <li>with every readme.md generation(from manual readme.generation or manual release) for every plugin an .md file gets generated in this folder, containing links to all image files of that plugin. the link to it is shown in the plugin template with the '%pluginmd%' variable.</li>
</ul>

screenshots/
<ul>
  <li>if you have screenshots put them into the screenshot folder and name them after the plugin. i.e. example.plugin01.jpg, example.plugin02.jpg ... these screenshots are shown in the plugin template with the '%screenshots%' variable</li>
</ul>

## advertising your plugins
<ul>
  <li>copy the link from the README's pluginlist table to get an anchorlink, that directly points to this special plugin. to add plugins to hecter's repo scroll down the release page to the first release, called 'Latest', and copy the zip link. every release renews these links, so they are always the same, while the version releases change. unfortunately the official repo currently doesn't support mulyi-plugin-repos. i have an open issue there and hope that it get supported in the future. feel free to post there to increase the pressure for fixing that.</li>
</ul>


## working with this repository

if you upload a new plugin, or update an existing, wait for the spell and script check in case there are errors you want to correct. then run the 'create release' workflow, and a minute later the plugin is released and the README is updated.

if you just want to change the static content of the upper part of the README or change the plugin template, edit res/template.txt, and run the 'make md' workflow. a minute later the new README is updated.

that is all. everything else is automated.
