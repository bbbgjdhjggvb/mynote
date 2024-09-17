1.  派生于`testing::Test`
2.  开头必须写`protectes:`
3. 然后就是对象，这个对象可以是测试的数据，测试的对象
4. 必须使用TEST_F函数不能用TEST
	1. TEST_F函数的第一个参数必须是fixtures这个类的名字
	2. 每个TEST_F共享一个fixtures类对象
5. 