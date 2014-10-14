# My Watir Cheat Sheet

This is my Cheat Sheet for using Watir:
Some of it may not make sense, don't worry

### So where do you want to start M8?
> I want to start by getting it going!

Well, you got to do this:
```ruby
require 'watir'
browser = Watir::Browser.new :firefox
```
>I got a browser window open, now what?

Well, I assume you want to go to a specific website!
```ruby
browser.goto "https://www.yoursite.com"
```
> Well, that was easy!

Yup, that is the easy part done. Now it all depends on what you want to do next!

> I don't know, just put down what you know!

Okay, will do.

### Email + Password Login

Use this, this will cover most email logins

```ruby
browser.text_field(id: "signup_email").when_present.set "email"
browser.text_field(id: 'signup_password').when_present.set 'password'
browser.button(:id, "signup_forms_submit").click
```

### Elements
Use this to find generic parts of web page

| Elements              | How to Access it?                             | Working with it                           |
| --------------------- | --------------------------------------------- | ----------------------------------------- |
| Text Box or Text Area | t = browser.text_field(:name, 'username')     |t.set "test"                               |
| Button                | b = browser.button(:value, 'Click Here')      |b.click                                    |    
| Link                  | l = browser.link(:url, "http://google.com")   |l.click                                    |
| Drop-Down List        | d = browser.select_list(:name, /country/)     |d.select 'UK'                              |
| Check Box             | c = browser.checkbox(:id, /unsubscribe/)      |c.set / c.clear                            |
| Radio Button          | r = browser.radio(:name, button_name)         |r.set / r.clear                            |
| Table                 | tbl = $ie.table(:id, /grades/)                |tbl[row][col].method e.g. tbl[2][1].text   |

> But dude, that seems like a lot of things. What happens if I can't see what it is that I've seleceted?

Hahah, Well, how you would you expose it?

> Umm,

```ruby
element.flash
```

> :O

Show me the money >:D OR better yet, show me what you can see

### Checking Contents:

```ruby 
browser.html # return html of page or element
browser.text # return text of page or element
browser.text.include? 'Pickaxe' # return true if the text appears on the page
browser.table(:id, 'jukebox_listing').to_a # return contents of a table as an array
browser.show_frames # identify the frames on a page
browser.text_fields.show # show info for all elements of a particular type on a pag
```
                                                                        
> Phew, that's a lot. Im gonna need some space

Let me Resize that for you

```ruby
browser.window.resize_to 1600, 1200
```

> Much better

Time for a selfie, let me take a look at you

```ruby
browser.screenshot.save "screenshot.png"
```


#### Random Methods
```ruby
require 'watir'
browser = Watir::Browser.new
browser.methods - Object.new.methods
browser.goto "http://google.com"
browser.goto "http://lacedeamon.spartaglobal.com/example_forms"
browser.back #back on page
browser.forward  #forward one page
browser.text
browser.text.include? "no" # Does the page contatin the word no?
browser.status
browser.text_field :name, "name" #looks like a hash, first takes symbol, second takes string
t = browser.text_field :name, /n.+/ # can use regex////use by name
t.flash # flashes the seleceted area
t.set "hello" # places the hello within the field box element
t.value
t.id
t.name
t.tab_index
t.attribute_value "tabindex"
t.exists? # does this html element exist within the page
browser.text_field(:name, /hello.+/).exists? # Does this element exist within the page
t.visible?
t.present? #needs to exist and be fully rendered
t.readonly? # see if the text field is read only
t.disabled?
t.enabled?

button = browser.button :text, "A Button"
button.text
# Much better to match by ID/Class but can use if needed
button.type
button.click
button.when_present.click # waits until present in page
browser.button(:text, "A Button").when_present.tab_index == 1
# type of explicit wait ^
d = browser.select_list :id, "select-choice"
d.select "Choice 3"
d.clear #clears selection on multi choice boxes

c=browser.checkbox :name, "checkbox"
c.set #check checkbox
c.clear

r = browser.radio :name, "radio-choice-12"
r.set

l = browser.link :href, "/writing/articles"
l.text
l.click

browser.link(:text, "About").click

browser.goto "http://lacedeamon.spartaglobal.com/contactform"
td = browser.table # finds the first table in the page
td.class
td[0].class
td[0][1] #gets the cells of the table
td[0][1].text #gets the text within the cell

browser.div :css ".f" # doesn't work well
browser.element(css: ".page-header").text
browser.element(css: ".page-header").html
browser.element(css: ".page-header h1").text
browser.element(css: ".page-header h1").html

browser.element(css: "p") # only returns 1 or the first "p" element
browser.elements(css: "p") # only returns multiple "p" element

ps = browser.elements(css: "p")
ps[2].text
ps[0].text
ps.size
ps.class
ps.element_class

browser.buttons # returns all buttons
browser.buttons.size
browser.buttons.to_a
browser.buttons.each {|b| puts b.text} # loops through buttons

browser.goto "http://danny.is/about"
ph = bowser.header :class, "page-header"
ph.flash
ph.nav.list # gets the first nav element/list
ph.nav.list.to_a
ph.nav.list.last #gets last bit of array
ph.nav.lis.last.a
ph.nav.lis.each {|li| puts li.a.href} # getting data out of page
#find the page header, find the nav element, get  the list, and for each element within the list, loop through and print out the list
#container class

###################################################################
browser.driver # tells us the driver
browser.driver.manage
browser.driver.manage.class
browser.class
browser.driver.class # were now back in selenium
browser.manage.implicit_wait = 5 #seconds

browser = Watir::Browser.start 'bit.ly/watir-webdriver-demo' #starts and go to url
browser.text_field(id: 'entry_0').when_present.set 'your name'
browser.text_field(id: 'entry_1000000').when_present.set 'your name'

browser.select_list(id: 'entry_1').wait_until_present
browser.button(:value => 'Submit').wait_while_present

wait = Watir::Wait
wait.until do
	browser.text.include? "thank you"
end

browser.close
# we can chain stuff together
#css selector can search by va
```