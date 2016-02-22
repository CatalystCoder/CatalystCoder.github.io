
---
title: Defining our Code
---

require'dictionary' #this is how we import our dictionary into the method. It brings in all our words.

def segment_string(str)
  i = 0 #Sets our content variable for the while loop aka the variable used to count our loop runs.
  index = -1 #sets the variable to anchor our search.
  cut = 1 #this variable gradually increases to test string against dictionary.
  arr = [] #This creates an empty array that we fill with our new words we find.

  if valid_word?(str) #string is a word.
    arr << str #Adds the string to the empty array we created.

  else #more complex.
    while i < str.length #beginning of the loop. What it states is that while our variable "i" is less than that of the string length, the loop will continue to run.
      test_word = str[index, cut] # This creates the variable that we'll be testing against to see if the string we cut off is a word.

      if valid_word?(test_word) #If the test is a valid word, do this.
        arr << test_word #adds test words to the array.
        index -= 1 #moves our anchor left from the last/first letter of the foudn word. The anchor simply being our place in the string. For example if we had "onetwothree" and the anchor was here "onetwothre|e" it would move the anchors placement, progressively back like this "onetwothr|ee", "onetwoth|ree" and so on until we get "onetwo|three" and the word is now located.
        cut = 1 #resets the number of letters we're cutting off / removing. The cut is the exact opposite of the index, numbers wise. It chooses how many numbers we have cut and this portion resets it back to one so that it can count up again to find the next word. Even though our index keeps going up, our cut resets to one once we find a working word with our dictionary.
        i +=1 #advance the loop count by one. 
      
      else valid_word?(test_word) == false #If the test isn't a valid word, do this process below. The process below is what moves our index and cut along. an example of it is in the index description above.
        index -= 1 #Moves the anchor to the left. Again, if we had "onetwothree" it would go like this after the first run "onetwothre|e".
        cut += 1 #cut off one more letter. This is what cuts that "e" from the word "three" above. It's what takes those letters and tries it against the dictionary. 
        i +=1 #advance the loop count by one.

      end #ends the if/else loop.
    end #ends the while loop.
  end #ends the larger if/else loop.
  arr.reverse #This organizes the order of the array. Since we were going from the left we need to put them in the correct order so instead of getting "three two one", the .reverse makes it come out as "one two three". This is only a display. To actually change it, you have to do arr.reverse!.
end #ends the defined method.
puts segment_string("onetwothree") #Calls the method we just defined and passes an argument to it.