# UI—第四弹，有趣的列表标签

##一、功能：
####1、按姓氏首字母将列表分组。
####2、滑动时，分组标签的重绘。

##二、微信公众号：
**关注微信公众号，获取密码，了解更多。**
**微信公众号：jike_android**
![公众号](https://github.com/wch0620/StatusBar/raw/master/WeiXin/qrcode.jpg)

##三、效果图：
![效果图](https://github.com/wch0620/StatusBar/raw/master/gif/label.gif)

###四、实现：

###1. 数据的获取：
####实际项目中，需要得到所有联系人的姓的首字母，然后进行分段，得到所有的标签。我这边并没有做数据库，只是模拟了数据。

```
		int length = Constant.LAST_NAME.length;
		mDisablePositions = new int[Constant.GROUP_LABELS.length];
		for (int i = 0; i < length; i++) {
			int size = (int) (Math.random() * 10 + 1);
			mDisablePositions[i + 1] = count;
			count += size;
			
			for(int j = 0; j < size; j++) {
				int nameIndex = (int) (Math.random() * Constant.FIRST_NAME.length);
				mList.add(Constant.LAST_NAME[i] + Constant.FIRST_NAME[nameIndex]);
			}
		}
```
####mDisablePositions保存每一个新的标签的位置。
###2、实现列表：
####这个很简单，没什么可说的，只需要注意在每一个标签的开始显示标签即可。就是mDisablePositions数组的位置显示标签。

####用二分法快速检验当前pos十分在mDisablePositions数组中。

```
        int index = Arrays.binarySearch(mDisablePositions, position);
        if (index >= 0) {
            return Constant.GROUP_LABELS[index];
        } else {
            return "";
        }
```

###3、列表滑动：

####主要是距离的计算。
```
View child = getChildAt(position - getFirstVisiblePosition());
if (child == null) {
	return;
	}
int childTop = child.getTop();
int deltaOffset = mListViewBaseOffsetTop - childTop;
```