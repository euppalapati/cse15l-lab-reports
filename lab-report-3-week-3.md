## Part 1
***

    import java.io.IOException;
    import java.net.URI;
    import java.util.ArrayList;

    class Handler implements URLHandler {
      ArrayList<String> strings = new ArrayList<String>();
  
      public String handleRequest(URI url) {
        String returnString = "";
    
        if(url.getPath().equals("/")) {
          for(int i = 0; i < strings.size(); i ++) {
            returnString += strings.get(i) + " ";
          }
      
         return returnString;
        }
  
        else if(url.getPath().equals("/search")) {
          String returnString2 = "";
          ArrayList<String> queryStrings = new ArrayList<String>();
          String[] querySearch = url.getQuery().split("=");
    
          if(querySearch[0].equals("s")) {
            String substring = querySearch[1];
      
            for(int i = 0; i < strings.size(); i ++) {
              if(strings.get(i).contains(substring)) {
                returnString2 += strings.get(i) + " ";
              }
            }
          }
    
          return returnString2;
        }
  
        else {
         System.out.println("Path: " + url.getPath());
    
          if(url.getPath().contains("/add")) {
            String[] querySearch = url.getQuery().split("=");
      
            if(querySearch[0].equals("s")) {
              String stringToAdd = querySearch[1];
              strings.add(stringToAdd);
              return "String added!";
            }
          }
    
          return "404 Not Found!";
        }
      }
    }

    class SearchEngine {
     public static void main(String[] args) {
        if(args.length == 0) {
          System.out.println("Missing port number! Try any number between 1024 and 49151");
          return;
        }
    
        int port = Integer.parseInt(args[0]);
        Server.start(port, new Handler());
      }
    }
                                          
***

![empty query](no-query.png)

For the image above, no method is called. There are no relevant arguments. The relevant fields are the words already added, since they are displayed if no method is specified. If these values change, the new set of words will be printed on the screen when the page is reloaded.

![add hello](add-hello.png)

For the image above, the add method is called. The relevant argument is "add?". The relevant fields are "s=" and the word to be added (in this case, "hello"). If this value is changed, a different word will be added to the list when the page is reloaded, but the text on the screen will stay the same.

![search h](search-h.png)
![search hey](search-hey.png)

For the images above, the search method is called. The relevant argument is "search?". The relevant fields are "s=" and the word to be looked up (in these cases, "h" and "hey"). We can see that when these values are changed, different words are printed on the screen when the page is reloaded. Since none of the words in the list contained "hey," no words were printed with this search query, while two words were printed with the "h" search query.

## Part 2
