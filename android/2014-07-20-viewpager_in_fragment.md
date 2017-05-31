# fragment中使用viewpager嵌套fragment

## 代码

在父fragment中:

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_parent, container, false);
    }

    @Override
    public void onViewCreated(View view, Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);

        ViewPager mViewPager = (ViewPager) view.findViewById(R.id.viewPager);
        mViewPager.setAdapter(new MyAdapter(getChildFragmentManager()));
    }

    public static class MyAdapter extends FragmentPagerAdapter {

        public MyAdapter(FragmentManager fm) {
            super(fm);
        }

        @Override
        public int getCount() {
            return 4;
        }

        @Override
        public Fragment getItem(int position) {
            Bundle args = new Bundle();
            args.putInt(TextViewFragment.POSITION_KEY, position);
            return TextViewFragment.newInstance(args);
        }
    }

*注意在实例化 FragmentPagerAdapter 时要用 Fragment.getChildFragmentManager(). 而且在子 fragments 里不能调用  Fragment.setRetainInstance() , 否则会报错. [nested fragment][2]  



refs:  
[android-viewpager-cant-update-dynamically][1]  
[how-to-add-a-fragment-inside-a-viewpager-using-nested-fragment-android-4-2][2]  



[1]: http://stackoverflow.com/questions/10849552/android-viewpager-cant-update-dynamically
[2]: http://stackoverflow.com/questions/13379194/how-to-add-a-fragment-inside-a-viewpager-using-nested-fragment-android-4-2