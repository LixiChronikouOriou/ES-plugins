# **Zuckung's Endless Sky Plugin Repository Template**

## Instructions

<ul>
  <li>Upload this template for an automatized plugin repository to a newly created github repository. Be aware of hidden folders and files, and get sure that all of them are uploaded.</li>
  <li>Go to the repo's settings: actions > general
    <ul>
        <li>Activate 'Allow all actions and reusable workflows'</li>
        <li>Activate 'Workflow permissions' > 'Read and write permissions'</li>
    </ul>
  </li>
  <li>Edit the files .github/workflows/'(manual) create release.yml' and .github/workflows/'(manual) make md.yml'
    <ul>
      <li>Change 'git config user.name "zuckung"' to your github username.</li>
      <li>Change 'git config user.email "zuckung@gmx.de"' to your email</li>
    </ul>
  </li>
  <li>Remove myplugins/example.plugin/ and put your plugins into the myplugins folder. See the ES wiki on <a href='https://github.com/endless-sky/endless-sky/wiki/CreatingPlugins'>Creating Plugins</a> for how a plugin has to be structured. Name your plugin folder without spaces or special characters, use dots or no spaces (i.e. example.plugin, ExamplePlugin). That is because when releasing, github replaces special characters or spaces with a dot. If you don't use this naming convention the links might be wrong.</li>
  <li>Run '(manual) create release' workflow from the actions tab, type in the exact name of the plugin, and wait a minute. The release will be created and a new README.md will be written.</li>
  <li>You are done. Read the rest of this instructions to see how the files system works and what else you can do.</li>
</ul>

## Details on folders and files

**.github/workflows/'(manual) create release.yml'**
<ul>
  <li>This is the workflow you use for releasing a plugin. After the plugin was uploaded, go to the <i>Action</i> tab, click on this workflow, click <i>Run Workflow</i>, enter the exact plugin name (else it fails) and let it run (it takes a minute to finish). It puts out a release with an asset zip file and with an increasing version number, noted in /res/versioning.txt. This workflow also generates the readme.md in all plugins, screenshots, the newly generated asset zip and other data. So never edit the readme, it gets overwritten on release.</li>
</ul>    
    
**.github/workflows/(manual) make md.yml**
<ul>
  <li>This workflow is also run manually in case you want to change the readme without pushing a release. It does the same as the previous workflow just without the release. The readme's content (besides the variable content, like plugins, paths etc) is read out of res/template.txt.</li>
</ul>

**.github/workflows/(on push) spellcheck.yml**
<ul>
  <li>This workflow runs on every push and checks for spelling errors inside the whole repository. It fails if an error is found and shows where it is.</li>
  <li>.codespell.exclude and .codespell.words.exclude can be edited to whitelist words, currently filled with my excludes as an example.</li>
</ul>

**.github/workflows/(on push) data check.yml**
<ul>
  <li>This workflow runs on every push and checks for ES script errors inside the myplugins folder. It fails if an error was found and shows where it is.</li>
  <li>That is done by starting the game on the github server, loading the plugins and reporting the errors.</li>
</ul>

**myplugins/example.plugin**
<ul>
  <li>An example plugin to show you how it should look like.</li>
</ul>

**res/template.txt**
<ul>
  <li>From here comes the static readme.md content. This textfile is splitted into 2 parts, the upper static content, and the variable plugin template, separated by %plugin template below this line%'. Each plugin gets this plugin template written to the README. It works with variables like '%variablename%'. These get replaced on generation. both parts can be mixed in html and markdown, i.e '%description%' variable gets replaced by the content from about.txt, '%size%' by kb/mb size, '%readme%' by the plugin readme.md content etc.</li>
<li>Useable variables inside template.txt:<br>
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

**res/news.txt**
<ul>
  <li>When releasing a plugin a new entry is made automatically, but manual entries work too. To change something just edit this file and on next readme generation workflow the newsbox is updated. The last 10 news entries are shown in the plugin template with the %news% variable.</li>
</ul>

**res/versioning.txt**
<ul>
  <li>If the plugin version isn't in this textfile it gets written to it and set to version '1.0.0'. with every run it increases by '0.0.1'. Manually changing works, i.e. setting the version to something like '1.1.0' or' 2.4.0' in versioning.txt.</li>
</ul>

**res/src**
<ul>
  <li>Python files. No need to touch them. The news box or the plugin variables get their content structure from here.</li>
</ul>

**res/imagemd/**
<ul>
  <li>With every readme.md generation (from manual readme.generation or manual release) for every plugin a .md file is generated in this folder, containing links to all image files of that plugin. The link to it is shown in the plugin template with the '%pluginmd%' variable.</li>
</ul>

**screenshots/**
<ul>
  <li>If you have screenshots put them into the screenshot folder and name them after the plugin, i.e. example.plugin01.jpg, example.plugin02.jpg etc. These screenshots are shown in the plugin template with the '%screenshots%' variable.</li>
</ul>


## Advertising your Plugins

Copy the link from the README's pluginlist table to get an anchorlink, that directly points to this special plugin. To add plugins to Hecter's repo scroll down the release page to the first release, called 'Latest', and copy the zip link. Every release renews these links, so they are always the same, while the version releases change. Unfortunately the official repo currently doesn't support multi-plugin-repos. I have an open issue there and hope that it gets supported in the future. Feel free to post there to increase the pressure for fixing that.


## Working with this repository

If you upload a new plugin, or update an existing, wait for the spell and script check in case there are errors you want to correct. Then run the 'create release' workflow, and a minute later the plugin is released and the README is updated.

If you just want to change the static content of the upper part of the README or change the plugin template, edit res/template.txt, and run the 'make md' workflow. A minute later the new README is updated.

That's all. Everything else is automated.
