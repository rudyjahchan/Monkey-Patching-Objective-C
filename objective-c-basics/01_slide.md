!SLIDE 
# Monkey-Patching 
# Objective-C#

## Extending iOS SDK ##

!SLIDE
# Defining Classes #

    @interface MyObject : NSObject

    @end

!SLIDE
# Instance Variables == ivars #

    @interface MyObject : NSObject {
      @private
      NSUInteger count
      MySubObject* subObject;
    }

    @end

!SLIDE smaller
# Methods #

        @interface MyObject : NSObject {
          @private
          NSUInteger _count;
          MySubObject* _subObject;
        }

        + (Counter*) counter;
        - (void) increment;
        - (MySubObject*) subObject;
        - (void) setSubObject:(MySubObject*)subObject;
        
        @end

!SLIDE smaller
# Implementing Classes #

        @implementation MyObject

        ...

        - (MySubObject*) subObject {
          return _subObject;
        }

        - (void) setSubObject:(MySubObject*)subObject {
          _subObject = [subObject retain];
        }

        ...

!SLIDE smaller
# Properties #

        @interface MyObject : NSObject {
          @private
          NSUInteger count;
          MySubObject* subObject;
        }

        + (Counter*) myObject;
        - (void) increment;

        @property (nonatomic,retain) subObject;

        @end

!SLIDE
# Properties #

    myObject.subObject;

    myObject.subObject = aSubObject;

!SLIDE smaller
# Implementing Properties #

        @implementation MyObject

        ...

        - (MySubObject*) subObject {
          return _subObject;
        }

        - (void) setSubObject:(MySubObject*)subObject {
          _subObject = [subObject retain];
        }

        ...

!SLIDE smaller
# @synthesize #

    @implementation MyObject

    @synthesize subObject = _subObject;

    ...

    @end

!SLIDE smaller
# In fact ... #

        @interface MyObject : NSObject {
          NSUInteger count;
        }

        ...

        @property (nonatomic,retain) subObject;

        @end

