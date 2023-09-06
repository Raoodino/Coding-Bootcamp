import java.math.*;
import java.text.*;
import java.util.*;
import java.util.regex.*;
import lib.Morph;

public class Morpher {
    public static Morph morph(String word) {
// WRITE YOUR CODE HERE
Morph morph = new Morph();

//extract the prefix of the word
        String prefix = extractPrefix(word);
        morph.pos = getPartOfSpeech(prefix);

        String stem = word.substring(prefix.length());

          // For prepositions and conjunctions
        if (morph.pos.equals("R") || morph.pos.equals("C")) {
            morph.root = word;
            return morph;
        }
          //if it is pronoun -- then stem is the word remove its suffix (here use the word with the prefix)
        if (morph.pos.equals("PN")) {
            stem = word;
        }

        // Step 2: Get tense, if applicable
        if (!morph.pos.equals("R") && !morph.pos.equals("C")) {
            morph.tense = getTense(stem);
            if (!morph.tense.equals("PRES")) {
                stem = stem.substring(0, stem.length() - 1);
            }
        }

        char[] initialVowelInfo = getInitialVowel(stem);
        morph.number = getNumber(initialVowelInfo);
        morph.gender = getGender(initialVowelInfo);

        if (initialVowelInfo.length == 2) {
            stem = stem.replaceFirst(new String(initialVowelInfo), "e");
        } else {
            stem = stem.replaceFirst(String.valueOf(initialVowelInfo[0]), "e");
        }
        morph.root = stem;
        return morph;
    }

    // Helper methods
    private static String extractPrefix(String word) {
        String[] possiblePrefixes = {"u", "y", "a", "e", "i", "o"};
        //special case: a and aa; y and yu
        if(word.substring(0, 2).equals("aa")){
                return "aa";
        }
        if(word.substring(0, 2).equals("yu")){
                return "yu";
        }
        for (String prefix : possiblePrefixes) {
            if (word.startsWith(prefix)) {
                return prefix;
            }
        }
        return "";
    }

    private static String getPartOfSpeech(String prefix) {
        switch (prefix) {
            case "u": return "V";
            case "y": return "ADJ";
            case "yu": return "ADV";
            case "a": return "R";
            case "aa": return "C";
            //if no prefix, then it is noun
            case "" : return "N";
            default: return "PN";
        }
    }

    private static String getTense(String stem) {
        if (stem.endsWith("u")) return "PAST";
        if (stem.endsWith("y")) return "FUT";
        return "PRES";
    }

    private static char[] getInitialVowel(String stem) {
        char[] vowels = {'a', 'e', 'i', 'o', 'u'};
    for (int i = 0; i < stem.length(); i++) {
        for (char v : vowels) {
            if (stem.charAt(i) == v) {
                if (i + 1 < stem.length() && stem.charAt(i + 1) == v) {
                    return new char[]{v, v};
                } else {
                    return new char[]{v};
                }
            }
        }
    }
    return new char[]{};
}



    private static String getNumber(char[] initialVowel) {
        return initialVowel.length > 1 ? "P" : "S";
    }

    private static String getGender(char[] initialVowel) {
        switch (initialVowel[0]) {
            case 'e': return "N";
            case 'i': return "F";
            case 'o': return "M";
            default: return "N";
        }

}
}

