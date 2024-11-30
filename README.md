# range_map

Created by beneficii

Taken from https://stackoverflow.com/a/67064808

## Original Answer

Way back in 2013/2014, I created a range_map container class template modeled on the container class templates of the C++ standard library. Each item of the range_map is stored in a class template called range_map_item, which has 3 fields: the left bound, the right bound, and the stored item. (FYI, everything is in the beneficii namespace.) It to a large extent works like std::map, but does not wrap around it. I created my own rb-tree to manage its contents.

The way the ranges work are as follows. Each key covers a range like so:

[left bound, right bound)

Meaning, the left bound is part of the range, but the right bound is not.

Ranges cannot imperfectly overlap, that is you can't have a 2 ranges where this is true:

left1 < left2 < right1 < right2

If 2 ranges do overlap, one must be entirely a subrange of the other.

The iterators go through by the range bounds, rather than the ranges themselves. It can tell you if it's currently pointing to a left bound or a right bound.

I've done a fair amount of testing with it. I've been able to create BMP files created by iterating through a range_map with random ranges placed in it and displaying the result. It seems to basically work, but I can't guarantee it will 100% and I haven't touched it in over 5 years.

There's no documentation with it, but the functions required to interact with it work similarly to their C++ standard library container counterparts. I would use emplace() most often. You can just pass the left bound, the right bound, and the item to it. (FYI, the "encaps" parameter is for whether you want to encapsulate preexisting items if those happen to be subranges of the item you want to enter/create.) You can also use piecewise construction on emplace() as well. (Thanks to a blog I found online that taught me how to set that up.)

Here is a link to the library. You should keep it in the "beneficii" subfolder, and just place that subfolder in your include directory or project directory or whatever. Wherever the compiler can search for include files. The library is header-only, so there are no linking issues.

Here is a link to the download: