
#### 引言


甘特图是一种流行的项目管理工具，用于显示项目的进度和任务分配。它通过条形图显示任务的开始和结束时间，使项目经理能够直观地了解项目的整体情况。在Java开发中，JFreeChart是一个强大的开源图表库，能够生成各种类型的图表，包括甘特图。本文将详细介绍如何在Java中使用JFreeChart生成甘特图，并提供一个完整的代码示例。


#### 一、JFreeChart简介


JFreeChart是一个用于生成各种图表的Java类库。它支持多种图表类型，如饼图、柱状图、折线图、散点图以及甘特图等。JFreeChart具有高度的可定制性，能够满足各种复杂的图表需求。


#### 二、准备工作


在使用JFreeChart生成甘特图之前，需要完成以下准备工作：


1\.**引入JFreeChart库**：确保在你的Java项目中已经引入了JFreeChart库。你可以通过Maven来引入这个库。以下是Maven的依赖配置：



```
<dependency>
    <groupId>org.jfreegroupId>
    <artifactId>jfreechartartifactId>
    <version>1.5.3version> 
dependency>

```

确保在`pom.xml`文件中添加上述代码，并更新项目依赖。


2\.**创建Java项目**：在你的IDE中创建一个新的Java项目，并配置好Maven依赖。


#### 三、创建甘特图


创建甘特图的过程可以分为以下几个步骤：


1. **定义数据集**：在JFreeChart中，使用`GanttCategoryDataset`来存储任务信息。
2. **创建甘特图**：使用`ChartFactory.createGanttChart`方法根据数据集生成甘特图。
3. **显示甘特图**：将生成的甘特图显示在一个窗口中。


下面是一个详细的代码示例，展示了如何在Java中使用JFreeChart生成甘特图。


##### 1\. 定义数据集


首先，我们需要定义一个数据集来存储任务信息。在JFreeChart中，`GanttCategoryDataset`接口用于存储甘特图的数据。我们可以使用`DefaultGanttCategoryDataset`类来实现这个接口。



```
import org.jfree.data.gantt.Task;
import org.jfree.data.gantt.GanttCategoryDataset;
import org.jfree.data.gantt.DefaultGanttCategoryDataset;
import java.util.Date;
 
public class GanttChartData {
    public GanttCategoryDataset createDataset() {
        DefaultGanttCategoryDataset dataset = new DefaultGanttCategoryDataset();
 
        // 创建任务
        Task task1 = new Task("Task 1", new Date(2023, 9, 1), new Date(2023, 9, 10));
        Task task2 = new Task("Task 2", new Date(2023, 9, 5), new Date(2023, 9, 15));
        Task task3 = new Task("Task 3", new Date(2023, 9, 10), new Date(2023, 9, 20));
 
        // 添加任务到数据集中
        dataset.add(task1, "Project A", "Task 1");
        dataset.add(task2, "Project A", "Task 2");
        dataset.add(task3, "Project A", "Task 3");
 
        return dataset;
    }
}

```

在这个示例中，我们创建了一个`GanttChartData`类，并在其中定义了一个`createDataset`方法。这个方法创建了一个`DefaultGanttCategoryDataset`对象，并添加了三个任务到数据集中。每个任务都有一个名称、开始日期和结束日期。


##### 2\. 创建甘特图


接下来，我们使用`ChartFactory.createGanttChart`方法根据数据集生成甘特图。



```
import org.jfree.chart.ChartFactory;
import org.jfree.chart.ChartPanel;
import org.jfree.chart.JFreeChart;
import javax.swing.*;
import java.awt.*;
 
public class GanttChartExample extends JFrame {
    public GanttChartExample(String title) {
        super(title);
 
        // 创建数据集
        GanttCategoryDataset dataset = new GanttChartData().createDataset();
 
        // 创建甘特图
        JFreeChart chart = ChartFactory.createGanttChart(
                "Task Schedule",    // 图表标题
                "Task",             // 任务轴标签
                "Date",             // 时间轴标签
                dataset,            // 数据集
                true,               // 显示图例
                true,               // 显示工具提示
                false               // 不显示 URL
        );
 
        // 创建和设置图表面板
        ChartPanel chartPanel = new ChartPanel(chart);
        chartPanel.setPreferredSize(new Dimension(800, 600));
        setContentPane(chartPanel);
    }
 
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            GanttChartExample example = new GanttChartExample("Gantt Chart Example");
            example.setSize(800, 600);
            example.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
            example.setVisible(true);
        });
    }
}

```

在这个示例中，我们创建了一个`GanttChartExample`类，它继承自`JFrame`。在构造函数中，我们首先创建了数据集，然后使用`ChartFactory.createGanttChart`方法生成甘特图。最后，我们将甘特图显示在一个`ChartPanel`中，并将其设置为窗口的内容面板。


在`main`方法中，我们使用`SwingUtilities.invokeLater`来确保GUI更新在事件调度线程中进行。然后，我们创建一个`GanttChartExample`对象，并设置窗口的大小、关闭操作和可见性。


##### 3\. 运行代码


将上述代码保存为两个Java文件：`GanttChartData.java`和`GanttChartExample.java`。确保你的项目已经正确配置了JFreeChart依赖。然后，运行`GanttChartExample`类的`main`方法。你将看到一个窗口显示生成的甘特图，其中包含了三个任务及其开始和结束时间。


#### 四、代码解析


以下是代码的详细解析：


1\.**导入语句**：



```
import org.jfree.chart.ChartFactory;
import org.jfree.chart.ChartPanel;
import org.jfree.chart.JFreeChart;
import org.jfree.data.gantt.Task;
import org.jfree.data.gantt.GanttCategoryDataset;
import org.jfree.data.gantt.DefaultGanttCategoryDataset;
import org.jfree.ui.ApplicationFrame; // 注意：这里我们使用JFrame而不是ApplicationFrame
import javax.swing.*;
import java.awt.*;
import java.util.Date;

```

导入必要的JFreeChart和Swing包，以便使用图表和创建窗口。


2\.**GanttChartData类**：



```
public class GanttChartData {
    public GanttCategoryDataset createDataset() {
        // ...（同上）
    }
}

```

定义一个`GanttChartData`类，并在其中创建数据集。


3\.**GanttChartExample类**：



```
public class GanttChartExample extends JFrame {
    // 构造函数（同上）
 
    public static void main(String[] args) {
        // ...（同上）
    }
}

```

定义一个`GanttChartExample`类，继承自`JFrame`。在构造函数中创建数据集和甘特图，并将其显示在窗口中。在`main`方法中，创建并显示甘特图窗口。


#### 五、自定义和扩展


JFreeChart提供了丰富的自定义和扩展功能。你可以根据需要调整图表的样式、添加交互功能、处理鼠标事件等。以下是一些常见的自定义选项：


1. **调整样式**：使用`JFreeChart`对象的`getPlot()`方法和`Plot`子类的方法来调整图表的样式，如坐标轴标签、网格线、图例等。
2. **添加交互功能**：使用`ChartMouseListener`和`ChartPanel`的`addChartMouseListener`方法来处理鼠标事件，如点击、悬停等。
3. **导出图表**：使用`ChartUtilities`类将图表导出为图像文件（如PNG、JPEG）或PDF文件。


#### 六、实际应用


甘特图在项目管理中具有广泛的应用价值。通过甘特图，项目经理可以直观地了解项目的进度和任务分配情况。以下是一些实际应用的场景：


1. **项目进度管理**：显示项目的各个阶段和任务的开始和结束时间，帮助项目经理跟踪项目的进度。
2. **资源分配**：显示每个任务所需的资源（如人力、物力），帮助项目经理合理分配资源。
3. **风险管理**：显示项目的关键路径和潜在风险点，帮助项目经理识别和管理风险。


#### 七、结论


本文详细介绍了如何在Java中使用JFreeChart生成甘特图。通过定义数据集、创建甘特图和显示甘特图三个步骤，我们成功地生成了一个包含三个任务的甘特图。此外，我们还介绍了代码解析、自定义和扩展以及实际应用等方面的内容。希望本文对你学习Java图表绘制有所帮助。


 本博客参考[飞数机场](https://ze16.com)。转载请注明出处！
