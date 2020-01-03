## Introduction

Aya uses `.resx` files for localization. This means that to create a new localization you need to create a new `.resx` file named `Resources.xx-XX.resx`, where `xx-XX` is a language ID in `languagecode2-country/regioncode2` format. Examples: de-DE for German (Germany), fr-CA for French (Canada), fr-FR for French (France). 

It is recommended to create translations into common languages first, without taking into account the regions (e.g. de-DE, fr-FR), if you do not plan to use cultural features.

`.resx` file is an XML file and looks like this:

```xml
<data name="Update_CheckForUpdates" xml:space="preserve">
  <value>Check for updates</value>
</data>
<data name="Update_Status_FailedToCheck" xml:space="preserve">
  <value>Unable to check for updates</value>
</data>
<data name="Close" xml:space="preserve">
  <value>Close</value>
</data>
<data name="Settings_Language" xml:space="preserve">
  <value>Language</value>
</data>
<data name="Main_Scan" xml:space="preserve">
  <value>Scan...</value>
</data>
<data name="Licensing_DaysRemaining" xml:space="preserve">
  <value>{0} days remaining</value>
  <comment>e.g. 16 days remaining</comment>
</data>
<data name="Upgrade_InEditionOnly_p1_Feature" xml:space="preserve">
  <value>This feature is only available in</value>
  <comment>e.g This feature is only available in Advanced edition.</comment>
</data>
<data name="Upgrade_InEditionOnly_p2_Edition" xml:space="preserve">
  <value>edition.</value>
</data>
```

The `<data>` tag has the attribute `name`, which is the key, and the `<value>` tag, which contains the text for the translation. 

Some `<data>` tags also contain the `<comment>` tag. Usually, the comment provides an example of a result string to help the translator understand the meaning. The content of the `<comment>` tag does not need to be translated. 

Tags `<data>` with attribute `name` containing markers `p1...pN` are part of one line or one sentence. Usually there is a comment in the tag with the `p1` marker that shows an example of a resulting string consisting of several parts. Make sure that the concatenation is correct.

## Creating a translation

To create a translation, you need a reference file in the neutral language (English), from which the structure of the new file will be taken. The reference file must be cloned from [Aya repo](https://github.com/7room/aya).

The translation process is to assign a new value to the `<value>` tag within the `<data>` tag. You should not change the value of the attribute `name`.

The simplest translation algorithm is to create a copy of the reference `.resx` file, rename it into a file with the appropriate language ID and replace the reference lines with the translated ones. 

> Although the above described algorithm is a trivial one, we recommend using [Resx Resource Manager](https://github.com/tom-englert/ResXResourceManager) to make the translation process more convenient. 

Once the translation is complete, you will need to make a pull request with your translation.

## Editing an existing translation

Similarly, you can use the above technique to modify the existing `.resx` files, including the reference one.

If you noticed a typo in the text or know how to best paraphrase a sentence, feel free to edit the English reference file and send us a pull request.

## Testing a translation

This part is a tricky one. To test your translation you need a compiler of `.resx` files into satellite assembly. The satellite assembly must be placed in the `xx-XX` subfolder of Aya installation folder, where `xx-XX` is your language ID. 

We recommend using a tool called [Resxul](https://github.com/paulem/resxul). Get the installer [here](https://github.com/paulem/resxul/releases/latest), install it and select `Aya` profile. Next, select your `.resx` file (make sure that the file name contains the correct language ID). Compile the assembly and copy it to the corresponding folder.

After launching Aya, select the desired language and make sure that all the strings are displayed as expected. If the strings are too long, try to rephrase them, recompile the satellite assembly and check again. If you are unable to rephrase a sentence and the UI does not allow you to fit a line of larger size, please [create an issue](https://github.com/7room/aya/issues/new/choose) and we'll look at how to improve Aya in this particular case.

> If you are using Resxul, you can skip the step of copying the assembly to the folder and choosing the language in Aya. Simply specify the path to Aya in Resxul and select "Automatically start application after compilation" option.

> More information about Resxul can be found in [its repo](https://github.com/paulem/resxul).

## Maintaining a translation

Subscribe to the changes in [Aya repo](https://github.com/7room/aya) to be aware of when the reference file changes. Pull the changes. Use `git` to view changes and make necessary changes to your translation files. Then make a pull request.
