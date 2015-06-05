
## 问题

1.长按时是怎么显示选择框，并弹出复制粘贴Toolbar的？

``` Java
/**
* Call this view's OnLongClickListener, if it is defined. Invokes the context menu if the
* OnLongClickListener did not consume the event.
*
* @return True if one of the above receivers consumed the event, false otherwise.
*/
public boolean performLongClick() {
    sendAccessibilityEvent(AccessibilityEvent.TYPE_VIEW_LONG_CLICKED);

    boolean handled = false;
    ListenerInfo li = mListenerInfo;
    if (li != null && li.mOnLongClickListener != null) {
        handled = li.mOnLongClickListener.onLongClick(View.this);
    }
    if (!handled) {
        handled = showContextMenu();
    }
    if (handled) {
        performHapticFeedback(HapticFeedbackConstants.LONG_PRESS);
    }
    return handled;
}
```

处理伪代码，但是往里面就不知道怎么看了
``` Java
// 伪代码 //
· android.support.v4.view.AccessibilityDelegateCompat.performAccessibilityAction
· android.support.v4.view.AccessibilityDelegateCompat.AccessibilityDelegateJellyBeanImpl.performAccessibilityAction
· android.support.v4.view.AccessibilityDelegateCompatJellyBean.performAccessibilityAction
// Delegate这种东东 //
· View.AccessibilityDelegate.performAccessibilityAction {
    // Note: Called from the default {@link AccessibilityDelegate} //
    performAccessibilityActionInternal {
        if (isLongClickable()) {
            performLongClick {
            	// A1.如果返回true，则不会调用A2 //
                A1.mOnLongClickListener.onLongClick() {
                	// 回调外层设置的监听 //
                }
                A2.showContextMenu {
                	getParent().showContextMenuForChild(this) {
                    	// 调用ViewParent的方法 //
                        ViewGroup.showContextMenuForChild
                    }
                }
                B.performHapticFeedback
            }
        }
    }
}
```

ViewGroup的这个方法就没看明白了
``` Java
// 自己调用自己吗？这里的mParent是谁？//
public boolean showContextMenuForChild(View originalView) {
    return mParent != null && mParent.showContextMenuForChild(originalView);
}
```

难道是调用了这个AbsListView的方法？
``` Java
@Override
public boolean showContextMenuForChild(View originalView) {
    final int longPressPosition = getPositionForView(originalView);
    if (longPressPosition >= 0) {
        final long longPressId = mAdapter.getItemId(longPressPosition);
        boolean handled = false;

        if (mOnItemLongClickListener != null) {
            handled = mOnItemLongClickListener.onItemLongClick(AbsListView.this, originalView,
                    longPressPosition, longPressId);
        }
        if (!handled) {
            mContextMenuInfo = createContextMenuInfo(
                    getChildAt(longPressPosition - mFirstPosition),
                    longPressPosition, longPressId);
            handled = super.showContextMenuForChild(originalView);
        }

        return handled;
    }
    return false;
}
```

