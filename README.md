Clone of the jquery plugin
[sheepit](http://www.mdelrosso.com/sheepit/index.php?lng=en_GB) that is hosted
at [google code](http://code.google.com/p/sheepit/). 

A post-removal callback has been added. This is useful for use with
`accepts_nested_attributes_for :items, :allow_destroy => true` in rails, so
that `:_destroy => '1'` can be set. Note: the parameter used to mark for
destroy is delete in rails 2.3 and destroy in 3.

If there's any interest in this, message me and I could maybe make rails
helpers.

Here's an example: 

    $('#sheepItForm').livequery(function(){
      $(this).sheepIt({
        afterRemove: function(index, formToRemove){
          // parse the removed form to extract rails Active Record item id. You'll 
          // need to add this class to your hidden input that has the id.
          var item_id = formToRemove.find('input.avatar_id').val();
          if (item_id){
            $('#sheepItForm_noforms_template').append(
              '<input type="hidden" name="member[avatars_attributes][][id]" value="' + item_id + '" />' +
              '<input type="hidden" name="member[avatars_attributes][][_destroy]" value="1" />'
            );
          }
        },
        data: avatars
      });
    });

I then also put:

    :javascript
      var avatars = #{@member.avatars.to_json(:only => [:id, :name])};

into my view (this is haml) so that the form is populated with has many items.
