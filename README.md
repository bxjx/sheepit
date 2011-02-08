Clone of the jquery plugin [sheepit](http://code.google.com/p/sheepit/). 

A post-removal callback has been added. This is useful for use with 
  accepts_nested_attributes_for :items, :allow_destroy => true
in rails, so that
  :_destroy => '1' 
will can be set. 
