!SLIDE smaller
# Reopening Classes (Category)#

        @interface NSDate (Helpers)

        - (NSString*) timeAgoInWords;

        @end

!SLIDE smaller
# Reopening Classes (Category) #

        @implementation NSDate (Helpers)

        - (NSString *)timeAgoInWords {
          double ti = [self timeIntervalSinceNow];
          ti = ti * -1;
          if(ti < 1) {
            return @"never";
          } else if (ti < 60) {
            return @"less than a minute ago";
          } else if (ti < 3600) {
            int diff = round(ti / 60);
            return [NSString stringWithFormat:@"%d minutes ago", diff];
          } else if (ti < 86400) {
            int diff = round(ti / 60 / 60);
            return[NSString stringWithFormat:@"%d hours ago", diff];
          } else if (ti < 2629743) {
            int diff = round(ti / 60 / 60 / 24);
            return[NSString stringWithFormat:@"%d days ago", diff];
          } else {
            return @"never";
          }   
        }

        @end

!SLIDE smaller
# SO ...#

        @interface UIViewController (Pager)

        @property (nonatomic,retain) 
            PagerController* pagerController;
        @property (nonatomic,retain) 
            ScrollTabBarItem* scrollTabBarItem;

        @end

        @implementation UIViewController (Pager)

        @synthesize pagerController;
        @synthesize scrollTabBarItem;

        @end

!SLIDE
# BUT ... #

!SLIDE
# Categories Can't Create 
# New ivars! #

!SLIDE
# What to do? #

!SLIDE smaller
# Associative References! #

        @implementation UIViewController (Pager)

        static char pagerControllerKey;
        static char scrollTabBarItemKey;

        - (PagerController *)pagerController
        {
          return (PagerController*)
              objc_getAssociatedObject(self,
                  &pagerControllerKey);
        }

        - (void)setPagerController:
            (PagerController *)pagerController
        {
          objc_setAssociatedObject(self, 
            &pagerControllerKey, 
            pagerController,
            OBJC_ASSOCIATION_RETAIN_NONATOMIC);
        }

        - (ScrollTabBarItem *)scrollTabBarItem
        {
          return (ScrollTabBarItem*)
            objc_getAssociatedObject(self,
              &scrollTabBarItemKey);
        }

        - (void)setScrollTabBarItem:(ScrollTabBarItem *)scrollTabBarItem
        {
          objc_setAssociatedObject(self, 
            &scrollTabBarItemKey, scrollTabBarItem,
            OBJC_ASSOCIATION_RETAIN_NONATOMIC);
        }
        @end
