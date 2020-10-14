# [1] Liquid Proficiency Questions

1. Describe how you would make a line of text in a homepage section editable from theme customization and how you would access this in liquid.
```
Create a .liquid file in the Section directory,
In {% schema %}, insert a block with { "type" : "text" }
```
2. How would you add the collection featured image as a banner on the collection liquid template?
```
In collection-template.liquid, use collection.image to access the featured image:
e.g: 
<div class="collection-hero">
  <div class="collection-hero__image"
     data-bgset="{% include 'bgset', image: collection.image %}"
     data-sizes="auto"
     data-parent-fit="cover"
     style="background-image: url('{{ collection.image | img_url: '300x300' }});">  
  </div>  
</div>
```
3. Using liquid code and HTML, create a simple pagination container, "< 1 2 ... 5 >".

```
{% paginate collections.all.products by 5 %}   
	{% for product in collections.all.products %}
		{{ product.id }} {{ product.title }} <br>
	{% endfor %} 
	{{ paginate | default_pagination: next: '>', previous: '<' }}
{% endpaginate %}
``` 

4. Using liquid code, access the product named "Blue T-Shirt". Store the id, title, handle, price, url, and image in variables.
```		    
{% assign title = all_products['blue-t-shirt'].title %}
{% assign id = all_products['blue-t-shirt'].id %}
{% assign handle = all_products['blue-t-shirt'].handle %}
{% assign price = all_products['blue-t-shirt'].price %}
{% assign url = all_products['blue-t-shirt'].url %}
{% assign imgArray = all_products['blue-t-shirt'].images %}
```	    
	    
5. Using liquid code, create a key:value array using the list below. Loop through the array. Upon key type, store the value in a variable to be used later:
		○ fruit:apple
		○ vegetable:carrot
		○ cloth:t-shirt
		○ denim:jeans
 
```
// since we can't create object in liquid. So the workout I'm using is to split key/val pairs into two arrays, and will retrieve value based on the key's index. 
    
{% capture string %}    
   fruit:apple,vegetable:carrot,cloth:t-shirt,denim:jeans    
{% endcapture %}
{% for json in string %}
  {% assign splitByComma = json | split: ',' %}
  {% for comma in splitByComma %}
    {% assign splitByDots = comma | split: ':' %}
    <p>key: {{splitByDots[0]}} {{ splitByDots[1] }}</p> 
    
    {% capture keys %}   
      {{keys}}{% if keys != '' %},{% endif %}{{splitByDots[0]}}
    {% endcapture %}

    {% capture values %}   
      {{values}}{% if keys != '' %},{% endif %}{{splitByDots[1]}}
    {% endcapture %}

  {% endfor %}
{% endfor %}

{%assign keys = keys | split: ','%}
{%assign values = values | split: ','%}

```
