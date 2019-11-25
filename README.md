This is my variation of `hadliq/LiveEvent`

The only difference is that my version has a pending flag such that if no observers have _ever_ observed a value the LiveEvent will hold it and emit it to the first observer.  Once observers start observing values then it emits a value.  New observers have to wait for the next value to be set.

The reason I did this was to work-around a race condition where it's possible to set an initial value in a LiveEvent before _any_ observers have started observing.  If that happened then in `hadliq`'s original implementation the event would be lost.  This introduced a lifecycle dependency to the LiveEvent I didn't like.

It should still emit a value just once.  But only once observers start observing.

I tried to PR it back to the original author but he didn't like my reasoning so I'm forking it.
