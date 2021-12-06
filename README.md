# Why-dont-we-reach-the-state-directly-in-NgRx

# QUESTION

currently I'm learning NgRx. So far I learned this:

For changing the state, we dispatch so called actions

An action is an object with an identifier and optionally with a payload

This action doesn’t directly reach the store, instead it reaches a so called reducer

The reducer is just a function: it gets the current state from the store and the action as an input

In the reducer we can have a look at the action identifier and perform the change on the state accordingly (which we got as an argument) to update that state, in an immutable way (changing the copy)

The reducer returns a new state, it returns a copy of the old state, and this state is forwarded to the app store

This reduced state is then overwriting the old state

I can't really understand, why we don't directly change the state stored in the store? Why do we need this reducer and make the change on a copy of the state in the store and write it back?


# ANSWER

For your first question as to why we do not directly change the state of your store. The answer is immutability

I think the key point that whole [action > reducer > store > selector] flow is immutability. It ensures the lack of any undesirable side effects and that your actions are predictable and repeatable.

This usually leads to improved performance and usually simpler programming and debugging.

As your application scales, the NGRX architecture will allow you to have a consistent and reliable state management.

Regarding pattern to follow, how we have to return the new state.
You just have to return a new state of the store. This helps to change to ensure a "new" value is always returned. Considering your reducer's state is an object, I think a "new" state helps refresh the value of your store and allows your application to know if there is a change made in the reducer.

A direct mutation of your state would not result in this refresh as described earlier.
