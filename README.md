public class EncodingTest {
	public static void main(String[] args) {
		System.out.println("=== 编码诊断信息 ===");
		System.out.println("1. 文件编码: " + System.getProperty("file.encoding"));
		System.out.println("2. 控制台编码: " + System.getProperty("console.encoding"));
		System.out.println("3. 默认字符集: " + Charset.defaultCharset());
		System.out.println("4. 系统语言: " + System.getProperty("user.language"));
		System.out.println("5. 系统地区: " + System.getProperty("user.country"));
		System.out.println("6. 操作系统: " + System.getProperty("os.name"));

		// 测试中文输出
		System.out.println("\n=== 测试中文输出 ===");
		System.out.println("中文测试: 你好，世界！");
		System.out.println("English Test: Hello, World!");

		// 显示所有系统属性
		System.out.println("\n=== 相关系统属性 ===");
		Properties props = System.getProperties();
		props.stringPropertyNames().stream()
			.filter(key -> key.toLowerCase().contains("encoding") ||
				key.toLowerCase().contains("lang") ||
				key.toLowerCase().contains("charset"))
			.sorted()
			.forEach(key -> System.out.printf("%-30s = %s%n", key, props.get(key)));
	}
}




when run application , console has messy code
貌似只加这段就OK
-Dfile.encoding=UTF-8 
-Duser.language=en 
-Duser.country=US 
-Dsun.jnu.encoding=UTF-8 
-Dsun.stdout.encoding=UTF-8 
-Dsun.stderr.encoding=UTF-8 
-Dconsole.encoding=UTF-8


方法1：修改IDEA运行配置（推荐）




点击运行按钮旁边的下拉箭头 → Edit Configurations

选择你的运行配置

在 VM options 中添加：

bash
-Dfile.encoding=UTF-8 -Duser.language=en -Dsun.jnu.encoding=UTF-8 -Duser.country=US
更完整的配置：
bash
-Dfile.encoding=UTF-8 
-Duser.language=en 
-Duser.country=US 
-Dsun.jnu.encoding=UTF-8 
-Dsun.stdout.encoding=UTF-8 
-Dsun.stderr.encoding=UTF-8 
-Dconsole.encoding=UTF-8
方法2：修改系统环境变量（Windows）
临时设置（CMD）：
cmd
set JAVA_TOOL_OPTIONS=-Dfile.encoding=UTF-8 -Duser.language=en -Dsun.jnu.encoding=UTF-8
永久设置：
系统属性 → 高级 → 环境变量

新建系统变量：

变量名：JAVA_TOOL_OPTIONS

变量值：-Dfile.encoding=UTF-8 -Duser.language=en -Duser.country=US -Dsun.jnu.encoding=UTF-8

重启IDEA





打开idea安装目录下的bin文件夹，找到idea.exe.vmoptions文件并打开
添加一条配置信息：-Dfile.encoding=UTF-8 
