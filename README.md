# SQL-by-code
Write SQL statement not using SQL but using programming language such as C, C++, Java, Python, etc.

# Using C language

```

innerJoin en JAVA

public String[][] innerJoin(String[][] R, int index1, String[][] S, int index2) {
    // temporary storage for matches
    ArrayList<String[]> matches = new ArrayList<>();

    // loop through both the tables to find out when the join column have common values.
    // output those common values.
    for (int i = 0; i < R.length; i++) {
        for (int j = 0; j < S.length; j++) {
            if (R[i][index1] == S[j][index2]) {
                matches.add(combine(R[i], S[j], index1, index2));
            }
        }
    }

    // convert matches to expected output array
    return matches.toArray(new String[matches.size()][]);
}

private String[] combine(String[] one, String[] two, int index1, int index2) {
    String[] r = new String[one.length + two.length - 1];
    int pos = 0;
    r[pos ++] = one[index1];
    for (int i=0; i<one.length; i++) if (i != index1) r[pos ++] = one[i];
    for (int i=0; i<two.length; i++) if (i != index2) r[pos ++] = two[i];
    return r;
}





3.5. Reading From CSV File
Now, let's try using StringTokenizer in a real use case.

There are scenarios where we try to read data from CSV files and parse the data based on the user-given delimiter.

Using StringTokenizer, we can easily get there:

public List<String> getTokensFromFile( String path , String delim ) {
    List<String> tokens = new ArrayList<>();
    String currLine = "";
    StringTokenizer tokenizer;
    try (BufferedReader br = new BufferedReader(
        new InputStreamReader(Application.class.getResourceAsStream( 
          "/" + path )))) {
        while (( currLine = br.readLine()) != null ) {
            tokenizer = new StringTokenizer( currLine , delim );
            while (tokenizer.hasMoreElements()) {
                tokens.add(tokenizer.nextToken());
            }
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
    return tokens;
}
Here, the function takes two arguments; one as CSV file name (i.e. read from the resources [src -> main -> resources] folder) and the other one as a delimiter.

Based on this two arguments, the CSV data is read line by line, and each line gets tokenized using StringTokenizer.

For example, we've put following content in the CSV:

1|IND|India
2|MY|Malaysia
3|AU|Australia
Hence, following tokens should be generated:

1
IND
India
2
MY
Malaysia
3
AU
Australia
3.6. Testing
Now, let's create a quick test case:

public class TokenizerTest {

    private MyTokenizer myTokenizer = new MyTokenizer();
    private List<String> expectedTokensForString = Arrays.asList(
      "Welcome" , "to" , "baeldung.com" );
    private List<String> expectedTokensForFile = Arrays.asList(
      "1" , "IND" , "India" , 
      "2" , "MY" , "Malaysia" , 
      "3", "AU" , "Australia" );

    @Test
    public void givenString_thenGetListOfString() {
        String str = "Welcome,to,baeldung.com";
        List<String> actualTokens = myTokenizer.getTokens( str );
 
        assertEquals( expectedTokensForString, actualTokens );
    }

    @Test
    public void givenFile_thenGetListOfString() {
        List<String> actualTokens = myTokenizer.getTokensFromFile( 
          "data.csv", "|" );
 
        assertEquals( expectedTokensForFile , actualTokens );
    }
}


```
