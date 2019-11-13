---
layout: post
title:      "Illustrations of Objects, Classes, & Instances [Ruby]"
date:       2019-11-12 19:00:33 -0500
permalink:  illustrations_of_objects_classes_and_instances_ruby
---


This post assumes you already read over some materials about Ruby's objects, classes, instances, variables, and methods. 

<hr>

I had a problem. Grasping the concept of "instance" confused me. At first I thought it made sense, but then  the Collaborating Objects Labs came along and I got lost. 

To solve that silly problem, I read/watched a bunch of other ruby docs and I made some visual notes to clarify how classes, objects, and instances all work together. 


## Below are some key bullet points.



![](http://giphygifs.s3.amazonaws.com/media/R4mn3MfNRmlCU/giphy.gif)




## What's the difference between class and object?



![](https://shill.lol/wp-content/uploads/2019/11/objects_everywhere.jpg)



* A class is a template for creating object instances. 
* Class tells ruby how to make an object of that particular type.
* If classes are cookie cutters, objects are the cookies they make. 
* You can write one class, and you can have many objects created by that one class.



![class_picture](https://shill.lol/wp-content/uploads/2019/11/cookie_cutter_class.jpg)



## What's an Instance?
* Think of "instance" as another way of saying "object". 
* An instance of a class is an object that was made using that class. You have to write one class, but you can have many instances of that class. 
* Again, just like that cookie cutter analogy. 



## What's an Instance Variable/Method?
* Instance *variables* are things that an object "**knows**" about itself.
* Instance *methods* are things that and object "**does**".
* There are also "Class methods/variable", but I won't go over that concept here. This post is just plain vanilla. Super basic.


![](https://shill.lol/wp-content/uploads/2019/11/class_eli5.jpg)




## Let's define a class to create many instances



![](https://shill.lol/wp-content/uploads/2019/11/rapper_instances.jpg)


From this example, we defined one Rapper class, and specify only ***once*** that rapper instances should have a name and age variables. But each Rapper ***object*** will have its own name and age, different from all other rapper ***instances***. 



### Show me thy code:



```

class Rapper

  attr_accessor :name, :age 

  def rap(rap_verse)
    puts "Yo, #{rap_verse}"
  end

  def dance 
    puts "I'm dancing, yo."
  end

  def make_it_rain
    puts "YOLO 🚀💸💰$$$💦☔️"
  end

end
 

```




Now everytime you summon `Rapper.new`, a new instance of a rapper is born! That's gangstah. 

Hope you learned a tiny bit from my horrible analogies. If not, it's cool too. Thanks for reading. 





