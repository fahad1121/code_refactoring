My Thoughts:

- Overall code is looking good as repository feature is applied that
  makes the code clean and seperate business logic with no more complex
  things in the controllers class. Using repository in laravel is the way
  to clean up the controller process so the code performance will be good

- I can see that you used the resource routing and controllers so you have
  some already available methods in controller but also you have placed other
  methods too. its not a good practice to use methods other than crud methods in
  resource controller because we have different routes format for resource controllers

- A controller class should contain only 8-10 functions with no duplication of the code

Code Change Recommendation：

1) BookingController.php:

- in function index（）， we don't need to assign a variable in if condition like
  "$user_id = $request->get('user_id')". by this way you are consuming the memory
  that we don't need anymore. we can simply check in if condition like "if($request->user_id)"
  that is more clean way to check
- $response = $this->repository->getUsersJobs($user_id);, this line calling a repository function if
  you look at this function in repository then there is conditionally based handling occurring like if
  and else if what about if controls could not enter into either of if block? what you will return in
  response? so there's a else block should be too there to handle exceptional cases.
- There's in the code you are getting values from env directly. first you should make a reference in
   config file to get values from env then you should call config values to approach env. in some cases,
   directly calling env could not work
- by calling getAll repo function you are passing request object to that function but in repository you
  are again declaring Request $request object which is not correct you are receiving everything in parameter
  so no need to declare it
- function should not exceed more than 10 lines for better performance. try to make small functions to call into
  your main function and increase the readability of code
- just return response  in if block if it doesn't need to check other then return response line should be not at the end
-  array_except($data, ['_token', 'submit']), you can use laravel of ignoring attributes like $request->except()
- this controller contains the code that is somehow same so you dont need to implement each method. you can create
  trait for this controller class and define methods there to avoid any repetition in future

2) BookingRepository.php:

- we dopn't need to give or re Declare models here. its already declared in controller class like did in current
  repository like "Request $request" dont need to add Request before $request
