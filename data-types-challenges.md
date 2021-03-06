# JavaScript Data Types Challenges
| Objectives |
| :--- |
| Identify 5 primitive data types and know when to use them |
| Explain the difference between primitive and reference data types |
| Explain the difference between dynamic and statically typed languages |
| Use the JS console to manipulate data and create objects |

## Challenges
1. Store your first name in a string variable
2. Concatenate your last name with your first name
3. Use [`split`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) to turn your string variable into an array
4. Use [`typeof`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof) to show how the output of [`split`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) is different from the input
5. Define a new array and concatenate the first and last elements


## Stretch Challenges
1. Explain why `null == undefined` and `null !== undefined` are both true statements.
2. Find a partner to exchange secret messages with
  * How you encode your message is up to you.
  * You might want to [convert your message to binary](http://www.binaryhexconverter.com/ascii-text-to-binary-converter) and/or use some built-in JS functions ([`slice`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice), [`replace`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace), etc) to obscure the data you are sending.
  * Get creative and make sure to include detailed instructions so that your partner knows how to decode the message.


#### Example
1. [Convert this binary data to text](http://www.binaryhexconverter.com/binary-to-ascii-text-converter):
```
01100001 01110111 01100101 01110011 01101111 01101101 01100101 00101100 00100000 01100100 01101111 01100111 01110011 00100000 01100001 01110010 01100101
```
2. Open the JS console and store the decoded string in a variable:
```
  var message = decoded_string_here;
```
3. Translate from yodaspeak to regular english:
```
  message = message.split(", ");
  message = message[1] + " " + message[0];
```


#### Extra Credit
Send the instructions for decoding via email and the message body via slack for extra security. How is this similar to public/private key cryptography?
