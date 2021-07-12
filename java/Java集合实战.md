###### 1.需求计算两个时间相差多少个小时，如果有相同的规则时间相加，不同则不加

> 第一种写法：只获取Name 名字，和 Hour小时

```java
public class Hour {
    public static void main(String[] args) throws ParseException {


        //设置日期格式
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        //定义开始时间
        Date date1 = sdf.parse("2019-10-01 10:12:15");
        List<ClassHor> list=new ArrayList<>();
        //添加数据
        list.add(new ClassHor(2,"小红",date1,new Date()));
        list.add(new ClassHor(3,"小戴",date1,new Date()));
        list.add(new ClassHor(1,"小王",date1,new Date()));
        list.add(new ClassHor(4,"小王",date1,new Date()));
        Map<String,Long> map=new HashMap<>();
        //循环list
        for (ClassHor list1: list) {
            String str1 = sdf.format(list1.getStartDate());
            String str2 = sdf.format(list1.getEndDate());
            Date d1 = sdf.parse(str1);
            Date d2 = sdf.parse(str2);
            //计算几个小时
             long  diff =  ((d2.getTime() - d1.getTime())/(1000 * 60 * 60));
            //检查key是否存在  Map上面是k String  V long
            if (map.containsKey(list1.getName())){
                long lo=map.get(list1.getName());
                map.put(list1.getName(),lo+diff);
            }else{
                map.put(list1.getName(),diff);
            }
        }
        //把Map转换List
        List<ClassHor> listl=new ArrayList();
        //迭代器
        Iterator<Map.Entry<String, Long>> iterator=map.entrySet().iterator();
        //while循环
        //hasNext:没有指针下移操作，只是判断是否存在下一个元素
        //next：指针下移，返回该指针所指向的元素
        //remove：删除当前指针所指向的元素，一般和next方法一起用，这时候的作用就是删除next方法返回的元素
        while(iterator.hasNext()) {
            Map.Entry<String, Long> map2=iterator.next();
            ClassHor lia=new ClassHor();
            lia.setName(map2.getKey());
            lia.setHour(map2.getValue().intValue());
            listl.add(lia);
        }


    }
    }

class ClassHor{
        private  int id;
        private  int hour;
        private  String name;
        private Date startDate;
        private Date endDate;

        public ClassHor() {

        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public ClassHor(int id, String name, Date startDate, Date endDate) {
            this.id = id;
            this.name = name;
            this.startDate = startDate;
            this.endDate = endDate;
        }

        public int getId() {
            return id;
        }

        public void setId(int id) {
            this.id = id;
        }

        public int getHour() {
            return hour;
        }

        public void setHour(int hour) {
            this.hour = hour;
        }

        public Date getStartDate() {
            return startDate;
        }

        public void setStartDate(Date startDate) {
            this.startDate = startDate;
        }

        public Date getEndDate() {
            return endDate;
        }

        public void setEndDate(Date endDate) {
            this.endDate = endDate;
        }
    }
```

> 第二种：获取全部VO里面的数据

```java 
public class Hour {
    public static void main(String[] args) throws ParseException {


        //设置日期格式
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        //定义开始时间
        Date date1 = sdf.parse("2019-10-01 10:12:15");
        List<ClassHor> list=new ArrayList<>();
        //添加数据
        list.add(new ClassHor(2,"小红",date1,new Date()));
        list.add(new ClassHor(3,"小戴",date1,new Date()));
        list.add(new ClassHor(1,"小王",date1,new Date()));
        list.add(new ClassHor(4,"小王",date1,new Date()));
        Map<String,ClassHor> map=new HashMap<>();
        //循环list
        for (ClassHor list1: list) {
            String str1 = sdf.format(list1.getStartDate());
            String str2 = sdf.format(list1.getEndDate());
            Date d1 = sdf.parse(str1);
            Date d2 = sdf.parse(str2);
            //计算几个小时
            long  diff =  ((d2.getTime() - d1.getTime())/(1000 * 60 * 60));
            //检查key是否存在  Map上面是k String  V long
            if (map.containsKey(list1.getName())){
                ClassHor vo=map.get(list1.getName());
                vo.setHour((int) (vo.getHour()+diff));
                map.put(list1.getName(),vo);
            }else{
                list1.setHour((int) diff);
                map.put(list1.getName(),list1);
            }
        }

        //把Map转换List
        List<ClassHor> listl=new ArrayList();
        //迭代器
        Iterator<Map.Entry<String, ClassHor>> iterator=map.entrySet().iterator();
        //while循环
        //hasNext:没有指针下移操作，只是判断是否存在下一个元素
        //next：指针下移，返回该指针所指向的元素
        //remove：删除当前指针所指向的元素，一般和next方法一起用，这时候的作用就是删除next方法返回的元素
        while(iterator.hasNext()) {
            Map.Entry<String, ClassHor> map2=iterator.next();
            ClassHor classHor=map2.getValue();
            listl.add(classHor);
        }
        //Java8 进行排序
      listl.sort(Comparator.comparing(ClassHor::getHour).reversed().thenComparing(ClassHor::getName));
        System.out.println( listl);
    }
}

class ClassHor {
    private int id;
    private int hour;
    private String name;
    private Date startDate;
    private Date endDate;
    public ClassHor() {

    }

    @Override
    public String toString() {
        return "ClassHor{" +
                "id=" + id +
                ", hour=" + hour +
                ", name='" + name + '\'' +
                ", startDate=" + startDate +
                ", endDate=" + endDate +
                '}';
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public ClassHor(int id, String name, Date startDate, Date endDate) {
        this.id = id;
        this.name = name;
        this.startDate = startDate;
        this.endDate = endDate;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public void setStartDate(Date startDate) {
        this.startDate = startDate;
    }

    public Date getEndDate() {
        return endDate;
    }

    public void setEndDate(Date endDate) {
        this.endDate = endDate;
    }

    public int getHour() {
        return hour;
    }

    public void setHour(int hour) {
        this.hour = hour;
    }

    public Date getStartDate() {
        return startDate;
    }


}
```

