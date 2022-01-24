# Baby-PHP-Writeup

Hey friends,

In this article I am going to share with you my writeup for the challenge **Baby PHP** from the SparkCTF.

Challenge Description :

This is a gift for the ones who didn't solve Evaluator!!!

[https://es1-ctf.herokuapp.com/ch4.php](https://es1-ctf.herokuapp.com/ch4.php) 

We are given this website which when we open we get a PHP code

![Untitled](https://user-images.githubusercontent.com/55143192/150676282-512e0d15-93b0-4c67-8756-b4d3ad63d77c.png)

Reading through the code we can see that we are dealing with `preg_replace` function that means anything we supply via the GET parameter other than [k?O!.o ] will be deleted. I spent quite a lot of time trying to figure out how to bypass this but I didn’t manage to get anything ( :3 ). However after reading the hint 

![2](https://user-images.githubusercontent.com/55143192/150676278-5b2fe5ef-00d8-449f-91b1-871f29026b02.png)

I found out the we are dealing with the Ook! language and that’s what those characters (k?O!.o) mean. So now we have the first half of the answer , now let’s think of the second half  and how we are going to make our payload in order to bypass the checks. 

The answer is this : [https://www.dcode.fr/ook-language](https://www.dcode.fr/ook-language) we should encode *peeehpeee* ( which is being compared with $y ) to the Ook! language. This comparison is done with the checker function which is originally found in the magic.php page , the checker function will decode our payload and if it finds it equal to peeehpeee it should print the flag.

Now let’s put together our payload .

After encrypting peeehpeee we get this

![3](https://user-images.githubusercontent.com/55143192/150676273-c916acdf-c88e-4174-b775-7c33a2e31937.png)

`Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook? Ook. Ook? Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook! Ook! Ook? Ook! Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook! Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook! Ook. Ook! Ook.
Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook? Ook. Ook? Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook! Ook! Ook? Ook! Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook! Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook! Ook. Ook! Ook.`

That’s what we need to supply as a GET parameter. 

The final payload is :

`?_=Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook? Ook. Ook? Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook! Ook! Ook? Ook! Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook! Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook! Ook. Ook! Ook.`

![4](https://user-images.githubusercontent.com/55143192/150676268-78827102-c1d3-41d4-9df1-290c76f8b10c.png)

Nani?! nothing prints out in the page , which is not the case in previous challenges.

At this point I thought my payload was wrong or something , but I took a look at the source code of the page. At first I didn’t see anything of interest.

![5](https://user-images.githubusercontent.com/55143192/150676248-362c8d96-3432-44c4-a8a3-c139ddab7642.png)

But when I hit ctrl+A to see if there is something hidden I found that there are whitespaces under the code.
![6](https://user-images.githubusercontent.com/55143192/150676305-0f97f5af-319d-4cac-8a0c-4aafc62a9555.png)

After doing some research I found something interesting in the CTF Katana of John Hammond github (https://github.com/JohnHammond/ctf-katana) specifically under the Steganography section. There is this thing called WhiteSpace

![Screenshot_4](https://user-images.githubusercontent.com/55143192/150676740-2b3d145c-5412-4bc4-b3fc-102e6f8133c8.png)

So I copy pasted the source code in the website https://tio.run/#whitespace and hit that execution button.

![Screenshot_3](https://user-images.githubusercontent.com/55143192/150676435-ada95165-3e83-4c20-b8b5-b20db40301d4.png)

Now if we go to the output we can see our flag :) ( It was missing an S at the beginning tho :P )

![8](https://user-images.githubusercontent.com/55143192/150676349-c91714e5-d283-4255-9dfd-27e3245e7354.png)

Flag : SP4RK{T#1s_1s_funny_1sn't!???}

Finally , I really enjoyed this challenge since it was a mix between web , cryptography and steganography. 

Thanks a lot for reading my writeup.

