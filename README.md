# UI�����ĵ�����Ȥ���б��ǩ

##һ�����ܣ�
####1������������ĸ���б���顣
####2������ʱ�������ǩ���ػ档

##����΢�Ź��ںţ�
**��ע΢�Ź��ںţ���ȡ���룬�˽���ࡣ**
**΢�Ź��ںţ�jike_android**
![���ں�](https://github.com/wch0620/StatusBar/raw/master/WeiXin/qrcode.jpg)

##����Ч��ͼ��
![Ч��ͼ](https://github.com/wch0620/StatusBar/raw/master/gif/label.gif)

###�ġ�ʵ�֣�

###1. ���ݵĻ�ȡ��
####ʵ����Ŀ�У���Ҫ�õ�������ϵ�˵��յ�����ĸ��Ȼ����зֶΣ��õ����еı�ǩ������߲�û�������ݿ⣬ֻ��ģ�������ݡ�

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
####mDisablePositions����ÿһ���µı�ǩ��λ�á�
###2��ʵ���б�
####����ܼ򵥣�ûʲô��˵�ģ�ֻ��Ҫע����ÿһ����ǩ�Ŀ�ʼ��ʾ��ǩ���ɡ�����mDisablePositions�����λ����ʾ��ǩ��

####�ö��ַ����ټ��鵱ǰposʮ����mDisablePositions�����С�

```
        int index = Arrays.binarySearch(mDisablePositions, position);
        if (index >= 0) {
            return Constant.GROUP_LABELS[index];
        } else {
            return "";
        }
```

###3���б�����

####��Ҫ�Ǿ���ļ��㡣
```
View child = getChildAt(position - getFirstVisiblePosition());
if (child == null) {
	return;
	}
int childTop = child.getTop();
int deltaOffset = mListViewBaseOffsetTop - childTop;
```