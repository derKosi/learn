Copilot Chat allows you to interact with Copilot using natural language. In this exercise, you'll use Copilot Chat to debug and improve code in the Trie project. Let's get started!

> [!IMPORTANT]
> This module requires the Github Copilot Chat extension, which is currently in public beta and subject to changes.

## Use Copilot Chat to debug code

1. Open the **Trie.cs** file

1. Navigate to the `LevenshteinDistance` method

    The Levenshtein distance is a method for measuring the differences between two strings. The Levenshtein distance between two strings is defined as the minimum number of edits needed to transform one string into the other. The edit operations include insertion, deletion, or substitution of a character.

    In this code, the Levenshtein distance is calculated incorrectly. Let's use Copilot Chat to fix the error.

1. Select all of the code for the `LevenshteinDistance` method

1. Right click the selected code. Under **Generate Code**, select **Review**

    Copilot should detect that the Levenshtein distance calculation is incorrect, and suggest incremental fixes.

1. Click **Apply and Go To Next** to apply the fixes and continue reviewing the code until all suggestions have been applied.

## Use Copilot Chat to improve code

You can use Copilot Chat to improve code by adding new features or refactoring existing code. Let's use Copilot Chat to improve the `PrintTrie` method.

1. Open the **Program.cs** file

1. Navigate to the `PrintTrie` method

    This method prints the contents of the trie to the console.

1. Select all of the code for the `PrintTrie` method

1. Right click the selected code and select **Inline Chat**

1. In the textbox, enter "Improve this code by separating the words into five columns"

1. Wait for Copilot to generate the new code.

    Copilot should suggest code that prints the words in five columns.

1. Click **Accept** to apply the changes.

## Check your work

In this task, you'll test the methods you created with Copilot to verify that they work as expected.

1. Open the **Program.cs** file

1. Uncomment the `GetSpellingSuggestions` method call:

    ```c#
    Trie dictionary = InitializeTrie(words);
    // SearchWord();
    // PrefixAutocomplete();
    // DeleteWord();
    GetSpellingSuggestions();
    ```

1. In the file explorer, right click the **Program.cs** file and click **Open in Integrated Terminal**

1. Enter ```dotnet run``` to run the program.

1. Enter a misspelled word to generate spelling suggestions for, such as "cae"

1. Verify that your output is similar to the following

    ```Output
    The dictionary contains the following words:
    as             cars           follows        monday         plans
    astronaut      cares          from           monster        the
    asteroid       careful        front          place          their
    are            carefully      mellow         plan           they
    around         for            mean           planet         there
    cat            forgot         money          planets        towards

    Enter a word to get spelling suggestions for, or press Enter to exit.
    cae
    Spelling suggestions for "cae":
    cat
    cars
    cares
    ```

    If your code displays different results, review your code to find your error and make updates. Run the code again to see if you've fixed the problem. Continue updating and running your code until your code produces the expected results.

1. Comment out the `GetSpellingSuggestions` method call.