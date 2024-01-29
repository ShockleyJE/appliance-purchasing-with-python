# Motivation

I recently moved and my apartment did not have a washer/dryer. There is coin laundry, but the value proposition is in a flux state of being *just* too inconvenient, *just* too unreliable, and *just* too expensive to consider a cheap set. 

My problem is that anything fitting that description does not stay on the market for long at all. It's not *quite* worth the opportunity cost of chasing down those deals, but it is worth executing on if an opportunity presents.

# Purpose

This project aims to solve a price discoverability challenge. When buying scratch/dented appliances, there's too many sites to check manually, and too many suppliers to stay up to tabs on. So, how can I just keep up to tab on the changes?

## Structure

This worksheet consists of Jupyter notebooks, some `.csv` files as temporary databases for reviewing in google sheets. The resources are described and executed in the following order

- [suppliers.ipynb](https://github.com/ShockleyJE/appliance-purchasing-with-python/blob/main/suppliers.ipynb) Input is your product requirements & distance, and output is effectively the '___ near me' sidebar results from google maps business search. However, the data is saved as csv and is easily able to be 1-click imported to google sheets where you can easily coordinate progress and perform ad-hoc filters with a partner. 


- [inventory_single.ipynb](https://github.com/ShockleyJE/appliance-purchasing-with-python/blob/main/inventory_single.ipynb) Input is a single website url from the `suppliers` dataframe. The notebook will to crawl the website and populate a dataframe with site routes where inventory location may be stored/ updated

- [inventory_full.ipynb](https://github.com/ShockleyJE/appliance-purchasing-with-python/blob/main/inventory_full.ipynb) Input is the full `suppliers` dataframe. The notebook will crawl all `suppliers` in the source dataframe. The output sheet contains columns [`monitor`, `acknowledged`] which represent whether the page has been reviewed manually and whether the row has had the default classification (that the link is not worth monitoring) overridden


## Optimizations 

- Take the list of sites to monitor from the classified `inventory_full` data frame on a cron interval and perform individual page scrapes, parse and deduplicate listing items, and store into a database

- Integrate with google calendars and have a new event created on a shared calendar whenever a new listing within our price range populates