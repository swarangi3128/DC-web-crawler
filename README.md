A web crawler, also known as a web spider or web bot, is a software program designed to systematically browse the internet and gather information from websites. While collecting URLs is a key aspect of what a web crawler does, its functions go beyond that. 
URL Discovery: Web crawlers start by visiting a set of seed URLs. From these initial URLs, they extract links to other pages on the same website and follow those links to discover new pages. This process continues, creating a map of the website's structure.

Content Extraction: Crawlers often extract various types of content from web pages, such as text, images, videos, and metadata. This collected information can be used for various purposes, such as indexing for search engines or data analysis.

Indexing: Search engines use web crawlers to index the content of web pages. This indexing enables search engines to quickly retrieve relevant results when users search for specific keywords or phrases.

Data Collection: Web crawlers can collect data for various purposes, including market research, sentiment analysis, price tracking, and more. They can be used to gather data on products, news, social media trends, and other relevant information.

Link Analysis: Crawlers analyze links between web pages to determine how pages are interconnected. This information is used by search engines to assess the importance of a page (PageRank in Google's case) and to help users discover related content.

Security Scanning: Web crawlers can be used to scan websites for vulnerabilities, security issues, or malware. This helps website owners identify and fix potential threats.


BELOW A COMPREHENSIVE EXPLAINATION HAS BEEN GIVEN ABOUT THE FUCNTIONING AND ROLE OF EACH PAGE.


MAIN:

Importing Modules: Importing necessary modules for multi-threading, queue management, and other functions.

Configuration Constants: Defining constants for the project name, homepage URL, and other settings.

Queue Initialization: Creating a queue to manage URLs for crawling.

Spider Initialization: Creating an instance of the Spider class with project and URL details.

Creating Worker Threads: Creating worker threads to process tasks concurrently.

Worker Function (work): Defining the work each worker thread will do.

Creating Jobs: Putting URLs from the queue file into the queue for processing.

Crawling Function (crawl): Checking if there are URLs in the queue and starting the crawling process.

Main Execution: Starting worker threads and initiating the crawling process.

The script combines these elements to create a multi-threaded web crawling process using the defined Spider class.
GENERAL:

create_project_dir(directory): Creates a directory (folder) for the web crawling project if it doesn't already exist.

create_data_files(project_name, base_url): Creates two data files (queue.txt and crawled.txt) within the project directory. If these files don't exist, queue.txt is initialized with the base_url, and crawled.txt is left empty.

write_file(path, data): Creates a new file at the given path and writes the provided data into it.

append_to_file(path, data): Adds the provided data as a new line to an existing file at the given path.

delete_file_contents(path): Clears the contents of an existing file, making it empty.

file_to_set(file_name): Reads the content of a file, converts each line into a set item, and returns the resulting set.

set_to_file(links, file): Takes a set of links and writes each link as a new line in the given file. It clears the file's contents before writing the new set of links.

These functions provide basic file and data management functionalities used by the web crawler. They handle creating and managing project directories, creating and updating data files (queue and crawled), as well as reading and writing sets of data (links) to and from files. These operations are essential for storing the state of the crawling process and the collected data.


LINK FINDER:

Importing Modules: Importing necessary modules for HTML parsing and URL handling.

Class Definition (LinkFinder):

Inherits from HTMLParser class for parsing HTML content.
Initializes with base_url (starting point of crawling) and page_url (current page being parsed).
Initializes an empty set self.links to store found links.
handle_starttag(tag, attrs) Method:

Called when the parser encounters an HTML start tag.
Checks if the tag is an anchor (<a>) tag.
Iterates through the tag's attributes.
If an attribute is 'href', constructs an absolute URL using urljoin() with base_url and the attribute's value.
Adds the absolute URL to the self.links set.
page_links() Method:

Returns the set of links found on the page.
error(message) Method:

A default error handling method for the parser. It's defined but left empty here.
This LinkFinder class is used to parse the HTML content of a page and extract all the absolute links (href attributes) from anchor (<a>) tags. The parsed links are stored in the links set, which can be accessed using the page_links() method. This class helps the crawler collect links from a page so that it can further explore and crawl those linked pages.


DOMAIN:

Importing Modules: Importing the urlparse function from the urllib.parse module for URL parsing.

get_domain_name(url) Function:

Returns the main domain name (like example.com) from a given URL.
Calls get_sub_domain_name(url) to get the full subdomain, splits it using '.', and constructs the main domain from the last two parts.
get_sub_domain_name(url) Function:

Returns the subdomain (like name.example.com) from a given URL.
Utilizes the urlparse() function to parse the given URL and extract the network location (netloc), which includes the subdomain.
These functions are used to extract domain and subdomain names from URLs. This can be important when categorizing URLs, determining link relationships, or distinguishing different parts of a website.

SPIDER:

Importing Modules: Importing necessary modules for URL handling, HTML parsing, and file operations.

Class Definition (Spider):

Defines a web crawler class with class-level variables for project-related information, queue, and crawled URLs.
The __init__ method initializes project details and starts crawling with the homepage URL.
boot() Method:

Creates project directories and initializes queue and crawled data from files.
crawl_page(thread_name, page_url) Method:

Crawls a page if not already crawled.
Displays crawling progress and updates queue and crawled sets.
Calls add_links_to_queue() and update_files().
gather_links(page_url) Method:

Fetches HTML content from a page, extracts and returns links using LinkFinder.
add_links_to_queue(links) Method:

Adds links to the queue if they meet certain criteria (not already queued, not already crawled, within the domain).
update_files() Method:

Updates queue and crawled data in their respective files.
Main Execution:

The script's main logic is within the class methods.
Overall, the Spider class orchestrates the crawling process. It starts from a given base URL, fetches HTML content, extracts links, adds valid links to the queue, and manages the crawling state. The class is responsible for maintaining the queue, crawled URLs, and data files.
