# Museum Post Image Scraper

This repository contains a Python code that is used to scrape images from museum posts on a select page.

## Usage

To use the code, clone the repository and run the `Museum_Post_Image_Scraper.ipynb` Jupyter notebook. The code begins by importing the necessary packages for scraping, such as lxml, requests, shutil, and os. It then defines the URLs of the two pages to be scraped. The code then uses the requests package to get the content of the page and the lxml package to parse the content into an xml tree. 

It then defines a function, `get_post_from_content`, which takes the xml tree and post number as parameters. This function uses xpaths to get the title and image URL of the post and returns them. Finally, it uses a `for` loop to iterate through all the posts on the page, calls the `get_post_from_content` function for each post, and downloads the images.

The code also contains two functions: `make_directory` and `download_image`. The `make_directory` function takes a title as an argument and creates a directory with the same name. It filters out any non-alphabetical characters from the title and replaces any spaces with underscores. The `download_image` function takes an image URL and the directory name as arguments, and downloads the image to the given directory. It uses the `shutil.copyfileobj` function to copy the raw data from the response object to an output file. Finally, the code uses a `for` loop to iterate over the post numbers and call the `get_post_from_content` and `download_image` functions to download the images for each post.

Example:

```
# Define the URLs of the pages to be scraped
url1 = 'http://www.example.com/museum-post-1'
url2 = 'http://www.example.com/museum-post-2'

# Get the content of the page
response1 = requests.get(url1)
response2 = requests.get(url2)

# Parse the content into an xml tree
tree1 = lxml.html.fromstring(response1.content)
tree2 = lxml.html.fromstring(response2.content)

# Iterate through all the posts on the page
for post_num in range(1, 10):
    post1 = get_post_from_content(tree1, post_num)
    post2 = get_post_from_content(tree2, post_num)
    
    # Create a directory for the post
    dir_name1 = make_directory(post1['title'])
    dir_name2 = make_directory(post2['title'])
    
    # Download the images
    download_image(post1['image_url'], dir_name1)
    download_image(post2['image_url'], dir_name2)
```

## Output

The code will create a directory for each post and download the images to the respective directories.