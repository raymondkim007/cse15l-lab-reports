# Lab Report 2 - Servers and Bugs

---

## Part 1 - StringServer

We will first create a web server that tracks a string that we can add to and edit.

The code for StringServer.java is shown below. 

    import java.io.IOException;
    import java.net.URI;

    class Handler implements URLHandler {
        String cur_string = "";

        public String handleRequest(URI url) {
            String query = url.getQuery();
            if (url.getPath().equals("/add-message")) {
                String[] parameters = query.split("=");
                if (parameters[0].equals("s")) {
                    cur_string += parameters[1] + "\n";
                    return String.format("String %s added to running string", parameters[1]);
                } else {
                    return "/add-message query requires input value";
                }
            } else {
                return cur_string;
            }
        }
    }

    class StringServer {
        public static void main(String[] args) throws IOException {
            if(args.length == 0){
                System.out.println("Missing port number! Try any number between 1024 to 49151");
                return;
            }

            int port = Integer.parseInt(args[0]);

            Server.start(port, new Handler());
        }
    }
---

## Remotely Connecting

### Creating a Git Bash Terminal

