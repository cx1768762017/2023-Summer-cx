1. 自我介绍
大家好!我是来自软件2102的陈星，
我热衷于学习不同的编程语言，包括C/java/python/C#等。喜欢解决问题时的逻辑思考过程。我对算法和数据结构也非常感兴趣，因为它们是构建高效软件系统的基础。
除了学术方面，我也注重实践能力的培养。我参与了一些软件开发项目，与团队合作，提高了我的沟通和协作能力。这些经历使我了解了如何将理论知识应用于实际项目中，并且意识到团队合作对于成功开发软件的重要性。
很高兴来到Gamecore游戏工作室，与大家共同学习游戏开发，期待与大家共同进步，携手做出一款属于自己的好游戏。


2. 最喜欢的游戏类型和一款游戏，以及原因    
最喜欢的游戏是坎巴拉太空计划。
它给我带来的不仅仅是逻辑，物理或者天文等知识的学习，它更是引发了我对梦想，对现实，以及对整个人生的思考。当你不畏艰难去完成一件事的时候，就像我第一次载着小绿人登陆月球的时候，收获得不仅仅是成功的喜悦，更是人生道路上的一次成长。
同时坎巴拉太空计划对模组的兼容性非常高，多种多样的模组带给我非常新奇的体验。


3.Unity中有哪些生命周期函数，它们各自在什么时候调用
- 加载第一个场景
  场景开始时将调用以下函数（为场景中的每个对象调用一次）。
  Awake：始终在任何 Start 函数之前并在实例化预制件之后调用此函数。（如果游戏对象在启动期间处于非活动状态，则在激活之后才会调用 Awake。）
  OnEnable：（仅在对象处于激活状态时调用）在启用对象后立即调用此函数。在创建 MonoBehaviour 实例时（例如加载关卡或实例化具有脚本组件的游戏对象时）会执行此调用。
  OnLevelWasLoaded：执行此函数可告知游戏已加载新关卡。
  请注意，对于添加到场景中的对象，在为任何对象调用 Start 和 Update 等函数之前，会为_所有_脚本调用 Awake 和 OnEnable 函数。当然，在游戏运行过程中实例化对象时，不能强制执行此调用。
- Editor
  Reset：调用 Reset 可以在脚本首次附加到对象时以及使用 Reset 命令时初始化脚本的属性。	  
- 在第一次帧更新之前
  Start：仅当启用脚本实例后，才会在第一次帧更新之前调用 Start。
  对于添加到场景中的对象，在为任何脚本调用 Update 等函数之前，将在所有脚本上调用 Start 函数。当然，在游戏运行过程中实例化对象时，不能强制执行此调用。
	  
- 帧之间
  OnApplicationPause：在帧的结尾处调用此函数（在正常帧更新之间有效检测到暂停）。在调用 OnApplicationPause 之后，将发出一个额外帧，从而允许游戏显示图形来指示暂停状态。
  
- 更新顺序
  跟踪游戏逻辑和交互、动画、摄像机位置等的时候，可以使用一些不同事件。常见方案是在 Update 函数中执行大多数任务，但是也可以使用其他函数。
  FixedUpdate：调用 FixedUpdate 的频度常常超过 Update。如果帧率很低，可以每帧调用该函数多次；如果帧率很高，可能在帧之间完全不调用该函数。在 FixedUpdate 之后将立即进行所有物理计算和更新。在 FixedUpdate 内应用运动计算时，无需将值乘以 Time.deltaTime。这是因为 FixedUpdate 的调用基于可靠的计时器（独立于帧率）。
  Update：每帧调用一次 Update。这是用于帧更新的主要函数。
  LateUpdate：每帧调用一次 LateUpdate__（在 Update__ 完成后）。LateUpdate 开始时，在 Update 中执行的所有计算便已完成。LateUpdate 的常见用途是跟随第三人称摄像机。如果在 Update 内让角色移动和转向，可以在 LateUpdate 中执行所有摄像机移动和旋转计算。这样可以确保角色在摄像机跟踪其位置之前已完全移动。
	  
- 动画更新循环
  Unity 评估动画系统时，将调用以下函数和 Profiler 标记。
  OnStateMachineEnter：在状态机更新 (State Machine Update) 步骤中，当控制器的状态机进行流经 Entry 状态的转换时，将在第一个更新帧上调用此回调。在转换到 StateMachine 子状态时不会调用此回调。
 
  仅当动画图中存在控制器组件（例如，AnimatorController、AnimatorOverrideController 或 AnimatorControllerPlayable）时才会发生此回调。
  注意：将此回调添加到 StateMachineBehaviour 组件会禁用多线程的状态机评估。
  OnStateMachineExit：在状态机更新 (State Machine Update) 步骤中，当控制器的状态机进行流经 Exit 状态的转换时，将在最后一个更新帧上调用此回调。在转换到 StateMachine 子状态时不会调用此回调。
  仅当动画图中存在控制器组件（例如，AnimatorController、AnimatorOverrideController 或 AnimatorControllerPlayable）时才会发生此回调。
  注意：将此回调添加到 StateMachineBehaviour 组件会禁用多线程的状态机评估。
  触发动画事件 (Fire Animation Events)：调用在上次更新时间和当前更新时间之间采样的所有剪辑中的所有动画事件。
  StateMachineBehaviour (OnStateEnter/OnStateUpdate/OnStateExit)：一个层最多可以有 3 个活动状态：当前状态、中断状态和下一个状态。使用一个定义 OnStateEnter、OnStateUpdate 或 OnStateExit 回调的 StateMachineBehaviour 组件为每个活动状态调用此函数。
  依次针对当前状态、中断状态和下一个状态调用此函数。
  仅当动画图中存在控制器组件（例如，AnimatorController、AnimatorOverrideController 或 AnimatorControllerPlayable）时才会执行此步骤。
  OnAnimatorMove：在每个更新帧中为每个 Animator 组件调用一次此函数来修改根运动 (Root Motion)。
  StateMachineBehaviour(OnStateMove)：使用定义此回调的 StateMachineBehaviour 在每个活动状态中调用此函数。
  OnAnimatorIK：设置动画 IK。为每个启用 IK pass 的 Animator Controller 层进行一次此调用。
  仅当使用人形骨架时才会执行此事件。
 StateMachineBehaviour(OnStateIK)：使用在启用 IK pass 的层上定义此回调的 StateMachineBehaviour 组件在每个活动状态中调用此函数。
  WriteProperties：从主线程将所有其他动画属性写入场景。
	  
- 渲染
  OnPreCull：在摄像机剔除场景之前调用。剔除操作将确定摄像机可以看到哪些对象。正好在进行剔除之前调用 OnPreCull。
  OnBecameVisible/OnBecameInvisible：对象变为对任何摄像机可见/不可见时调用。
  OnWillRenderObject：如果对象可见，则为每个摄像机调用一次。
  OnPreRender：在摄像机开始渲染场景之前调用。
  OnRenderObject：所有常规场景渲染完成之后调用。此时，可以使用 GL 类或 Graphics.DrawMeshNow 来绘制自定义几何形状。
  OnPostRender：在摄像机完成场景渲染后调用。
  OnRenderImage：在场景渲染完成后调用以允许对图像进行后处理，
  OnGUI：每帧调用多次以响应 GUI 事件。首先处理布局和重新绘制事件，然后为每个输入事件处理布局和键盘/鼠标事件。
  OnDrawGizmos 用于在场景视图中绘制辅助图标以实现可视化。
  
- 协程
  Update 函数返回后将运行正常协程更新。协程是一个可暂停执行 (yield) 直到给定的 YieldInstruction 达到完成状态的函数。 协程的不同用法：
  yield 在下一帧上调用所有 Update 函数后，协程将继续。
  yield WaitForSeconds 在为帧调用所有 Update 函数后，在指定的时间延迟后继续协程
  yield WaitForFixedUpdate 在所有脚本上调用所有 FixedUpdate 后继续协程
  yield WWW 在 WWW 下载完成后继续。
  yield StartCoroutine 将协程链接起来，并会等待 MyFunc 协程先完成。
  
- 销毁对象时
  OnDestroy：对象存在的最后一帧完成所有帧更新之后，调用此函数（可能应 Object.Destroy 要求或在场景关闭时销毁该对象）。
  
- 退出时
  在场景中的所有活动对象上调用以下函数：
  OnApplicationQuit：在退出应用程序之前在所有游戏对象上调用此函数。在编辑器中，用户停止播放模式时，调用函数。
  OnDisable：行为被禁用或处于非活动状态时，调用此函数。


4.其他笔记
# Unity学习笔记

## 编程

### C#

- C#的作用

  在Unity3D中，C#（C Sharp）是一种常用的编程语言，它是Unity支持的主要脚本语言之一。C#在Unity中有多种作用，包括：
  1. 游戏逻辑编写：使用C#编写游戏的逻辑和功能。可以创建游戏对象、处理输入、处理碰撞、实现游戏规则和行为等等。C#是一种强类型语言，可以提供更严谨的代码结构和更强大的功能。
  2. 组件和行为脚本：在Unity中，C#被用于编写组件脚本，通过将脚本组件附加到游戏对象上，实现自定义的行为和功能。这些组件可以控制对象的移动、动画、碰撞检测、触发事件等等。对于复杂的游戏功能，C#的面向对象编程特性可以提供更灵活的设计和组织方式。
  3. 用户界面和交互：C#可以用于编写游戏的用户界面和交互。通过使用Unity提供的UI系统，可以使用C#脚本控制UI元素的显示和隐藏、按钮点击事件、拖拽操作等等。
  4. 游戏性能优化：C#提供了一些性能优化的技术，可以在游戏中通过合理使用C#编写的代码来提高游戏的性能。例如，使用对象池技术来管理和重用游戏对象，使用协程来实现异步处理，使用线程来处理耗时操作等等。
  总之，C#在Unity3D中是一种强大而灵活的编程语言，可以用于实现游戏逻辑、自定义组件和行为、用户界面和交互，以及优化游戏性能。通过合理使用C#，可以让游戏开发者更高效、更快速地开发出高质量的游戏。
  
- 基本语法

	- 函数

	- 书写格式

	- 流程控制

		- if语句

		- 循环

			- for

			- while

			- do_while

			- for_each

		- switch语句

	- 变量和变量作用域（访问修饰符）

		- 在编辑器中修改公共变量

	- 数组

	- 枚举

- Unity方法

	- Awake 和 Start

		- Awake

		  在启动游戏时调用，即使还没有调用脚本组件
		  
		- Start

		  启动脚本组件后，在Awake之后，首次更新之前调用
		  
	- Update 和 FixedUpdate

		- Update 

		  每一帧都存在调用，用于实现输入检测、非物理对象的移动、简单计时器等功能
		  
		- FixedUpdate

		  按照固定时间调用，调用的时间间隔相同。
		  在调用函数后，立即计算刚体物体的运动。
		  
	- Vector3.magnitude（矢量数学）

	  用于矢量计算
	  
	  矢量数学涉及多种运算，其中一些常见的包括：
	  1. 矢量加法：将两个矢量的对应分量相加，得到一个新的矢量。例如，对于二维矢量a = (a1, a2)和b = (b1, b2)，它们的和为a + b = (a1 + b1, a2 + b2)。
	  2. 矢量减法：将一个矢量的对应分量减去另一个矢量的对应分量，得到一个新的矢量。例如，对于二维矢量a和b，它们的差为a - b = (a1 - b1, a2 - b2)。
	  3. 矢量数量乘法：将矢量的每个分量与一个标量（常数）相乘，得到一个新的矢量。例如，对于二维矢量a和标量c，它们的数量乘积为c * a = (c * a1, c * a2)。
	  4. 点积（内积）：将两个矢量的对应分量相乘，再将所有乘积相加，得到一个标量。例如，对于二维矢量a和b，它们的点积为a · b = a1 * b1 + a2 * b2。
	  5. 叉积（外积）：只适用于三维矢量。将两个矢量的对应分量进行交叉相乘，得到一个新的矢量。例如，对于三维矢量a和b，它们的叉积为a × b = (a2 * b3 - a3 * b2, a3 * b1 - a1 * b3, a1 * b2 - a2 * b1)。
	  
	  
	- Invoke、InvokeRepeating 和 CancelInvoke

		- Invoke

		  将函数调用安排在指定延迟之后发生
		  它的语法格式如下：
		  public void Invoke(string methodName, float time);
		  其中，methodName 是要调用的方法的名称，time 是要延迟的时间（以秒为单位）。
		  示例：
		  Invoke("MyMethod", 2.0f);
		  上述代码将在延迟 2 秒后调用 MyMethod 方法。
		  
		  
		- InvokeRepeating 

		  InvokeRepeating 函数用于以固定的时间间隔重复调用一个方法。它的函数签名如下：
		  public void InvokeRepeating(string methodName, float time, float repeatRate);
		  其中，methodName 是要调用的方法的名称，time 是要延迟的时间（以秒为单位），repeatRate 是重复调用的时间间隔（以秒为单位）。
		  示例：
		  InvokeRepeating("MyMethod", 2.0f, 3.0f);
		  上述代码将在延迟 2 秒后开始调用 MyMethod 方法，并每隔 3 秒重复执行一次。
		  
		- CancelInvoke 

		  CancelInvoke 函数用于取消之前使用 Invoke 或 InvokeRepeating 方法预定的所有方法调用。它的语法格式如下：
		  public void CancelInvoke();
		  示例：
		  CancelInvoke();
		  上述代码将取消之前预定的所有方法调用，停止它们的执行。
		  
		  
		  
	- Instantiate

	  在Unity中，使用Instantiate函数可以在运行时创建预制件的克隆体。Instantiate函数有多个重载版本，以下是常用的方式：
	  1. Instantiate(GameObject original)：创建原始游戏对象的克隆体。
	  GameObject clone = Instantiate(originalPrefab);
	  2. Instantiate(GameObject original, Vector3 position, Quaternion rotation)：可以指定克隆体的位置和旋转。
	  Vector3 position = new Vector3(0, 0, 0);
	  Quaternion rotation = Quaternion.identity;
	  GameObject clone = Instantiate(originalPrefab, position, rotation);
	  3. Instantiate(GameObject original, Transform parent)：将克隆体设置为指定父对象的子对象。
	  Transform parent = transform;
	  GameObject clone = Instantiate(originalPrefab, parent);
	  4. Instantiate(GameObject original, Vector3 position, Quaternion rotation, Transform parent)：同时指定位置、旋转和父对象。
	  Vector3 position = new Vector3(0, 0, 0);
	  Quaternion rotation = Quaternion.identity;
	  Transform parent = transform;
	  GameObject clone = Instantiate(originalPrefab, position, rotation, parent);
	  
	- 线性插值

	  在制作游戏时，有时可以在两个值之间进行线性插值。这是通过 Lerp 函数来完成的。线性插值会在两个给定值之间找到某个百分比的值。例如，我们可以在数字 3 和 5 之间按 50% 进行线性插值以得到数字 4。这是因为 4 是 3 和 5 之间距离的 50%。
	  在 Unity 中，有多个 Lerp 函数可用于不同类型。对于我们刚才使用的示例，与之等效的将是 Mathf.Lerp 函数，如下所示：
	  
	  // 在此示例中，result = 4
	  float result = Mathf.Lerp (3f, 5f, 0.5f);
	  Mathf.Lerp 函数接受 3 个 float 参数：一个 float 参数表示要进行插值的起始值，另一个 float 参数表示要进行插值的结束值，最后一个 float 参数表示要进行插值的距离。在此示例中，插值为 0.5，表示 50%。如果为 0，则函数将返回“from”值；如果为 1，则函数将返回“to”值。
	  Lerp 函数的其他示例包括 Color.Lerp 和 Vector3.Lerp。这些函数的工作方式与 Mathf.Lerp 完全相同，但是“from”和“to”值分别为 Color 和 Vector3 类型。在每个示例中，第三个参数仍然是一个 float 参数，表示要插值的大小。这些函数的结果是找到一种颜色（两种给定颜色的某种混合）以及一个矢量（占两个给定矢量之间的百分比）。
	  让我们看看另一个示例：
	  
	  Vector3 from = new Vector3 (1f, 2f, 3f);
	  Vector3 to = new Vector3 (5f, 6f, 7f);
	  
	  // 此处 result = (4, 5, 6)
	  Vector3 result = Vector3.Lerp (from, to, 0.75f);
	  在此示例中，结果为 (4, 5, 6)，因为 4 位于 1 到 5 之间的 75% 处，5 位于 2 到 6 之间的 75% 处，而 6 位于 3 到 7 之间的 75% 处。
	  使用 Color.Lerp 时适用同样的原理。在 Color 结构中，颜色由代表红色、蓝色、绿色和 Alpha 的 4 个 float 参数表示。使用 Lerp 时，与 Mathf.Lerp 和 Vector3.Lerp 一样，这些 float 数值将进行插值。
	  在某些情况下，可使用 Lerp 函数使值随时间平滑。请考虑以下代码段：
	  
	  void Update ()
	  {
	      light.intensity = Mathf.Lerp(light.intensity, 8f, 0.5f);
	  }
	  如果光的强度从 0 开始，则在第一次更新后，其值将设置为 4。下一帧会将其设置为 6，然后设置为 7，再然后设置为 7.5，依此类推。因此，经过几帧后，光强度将趋向于 8，但随着接近目标，其变化速率将减慢。请注意，这是在若干个帧的过程中发生的。如果我们不希望与帧率有关，则可以使用以下代码：
	  
	  void Update ()
	  {
	      light.intensity = Mathf.Lerp(light.intensity, 8f, 0.5f * Time.deltaTime);
	  }
	  这意味着强度变化将按每秒而不是每帧发生。
	  请注意，在对值进行平滑时，通常情况下最好使用 SmoothDamp 函数。仅当您确定想要的效果时，才应使用 Lerp 进行平滑。
	  
	- 组件引用、禁用、删除

		- GetComponet

		  使用`GetComponent`函数可以获取其他脚本或组件的引用，并通过该引用来访问和处理其属性。下面是使用`GetComponent`函数处理其他脚本或组件属性的步骤：
		  
		  1. 确定要访问的脚本或组件所附加的游戏对象。例如，假设你有一个名为`Player`的游戏对象上附加了一个名为`PlayerController`的脚本。
		  
		  2. 在需要访问其他脚本或组件属性的脚本中，使用`GetComponent`函数获取对应脚本或组件的引用。假设你要在一个名为`GameManager`的脚本中访问`PlayerController`的属性。
		  
		     ```csharp
		     PlayerController playerController; // 声明对应脚本或组件的引用
		  
		     void Start()
		     {
		         // 获取Player对象上的PlayerController组件
		         playerController = GetComponent<PlayerController>();
		     }
		     ```
		  
		  3. 通过获得的引用，你可以访问和修改该脚本或组件的属性。让我们假设`PlayerController`脚本有一个名为`speed`的属性，用于控制玩家对象的速度。
		  
		     ```csharp
		     void Update()
		     {
		         // 使用获得的脚本或组件引用访问和修改其属性
		         playerController.speed = 10f;
		     }
		     ```
		  
		  这样，你就可以使用`GetComponent`函数获取其他脚本或组件的引用，并通过该引用来访问和处理其属性。请确保在调用`GetComponent`函数时传入正确的脚本或组件类型，以便获得正确的引用。
		  
		  
		- 在运行时通过脚本启用和禁用组件

		  在C#中，可以使用代码在运行时启用和禁用组件。下面是一个简单的示例，演示如何通过脚本控制组件的启用和禁用：
		  ```csharp
		  using UnityEngine;
		  public class ComponentManager : MonoBehaviour
		  {
		      public GameObject component; // 要启用/禁用的组件
		      private void Start()
		      {
		          // 启用组件
		          EnableComponent(component);
		          // 延迟3秒后禁用组件
		          Invoke("DisableComponent", 3f);
		      }
		      private void EnableComponent(GameObject obj)
		      {
		          // 激活游戏对象上的组件
		          obj.SetActive(true);
		      }
		      private void DisableComponent()
		      {
		          // 禁用游戏对象上的组件
		          component.SetActive(false);
		      }
		  }
		  ```
		  在上面的示例中，我们创建了一个名为`ComponentManager`的脚本，并将需要启用/禁用的组件赋值给`component`变量。在`Start()`方法中，我们调用`EnableComponent()`方法启用组件，然后使用`Invoke()`方法来延迟3秒后调用`DisableComponent()`方法来禁用组件。
		  `EnableComponent()`方法使用`SetActive(true)`来激活传递的游戏对象上的组件，使其可见和可用。`DisableComponent()`方法使用`SetActive(false)`来禁用游戏对象上的组件，使其不可见和不可用。
		  你可以将上述示例代码添加到C#脚本中，并将该脚本附加到游戏对象上。当游戏运行时，脚本将会在启动后3秒内启用组件，然后禁用它。
		  请确保将`component`变量正确赋值为要启用/禁用的组件。根据你的需求，你可以在不同的时间点调用`EnableComponent()`和`DisableComponent()`方法，以实现动态控制组件的启用和禁用。
		  
		- 处理场景内部游戏对象的活动状态

		  在Unity中，可以使用`SetActive()`和`activeSelf`/`activeInHierarchy`来单独处理游戏对象的活动状态，以及在层级视图中处理场景内部游戏对象的活动状态。
		  1. 使用`SetActive()`方法：
		     - `SetActive(bool isActive)`方法用于启用或禁用游戏对象。将`isActive`参数设置为`true`将启用游戏对象，将其设置为`false`将禁用游戏对象。
		     - 例如，使用以下代码可以启用或禁用名为`component`的游戏对象：
		       ```csharp
		       component.SetActive(true); // 启用游戏对象
		       component.SetActive(false); // 禁用游戏对象
		       ```
		  2. 使用`activeSelf`和`activeInHierarchy`属性：
		     - `activeSelf`表示游戏对象自身是否处于活动状态，无论其父游戏对象的活动状态如何。
		     - `activeInHierarchy`表示游戏对象及其父游戏对象是否都处于活动状态。
		     - 例如，使用以下代码可以检查游戏对象的活动状态：
		       ```csharp
		       if (component.activeSelf)
		       {
		           // 游戏对象处于活动状态
		       }
		  
		       if (component.activeInHierarchy)
		       {
		           // 游戏对象及其父游戏对象都处于活动状态
		       }
		       ```
		  
		  在层级视图中处理场景内部游戏对象的活动状态：
		  1. 在Unity的层级视图中，可以手动启用或禁用游戏对象，以改变其活动状态。
		  2. 在层级视图中，启用的游戏对象将显示为亮色，而禁用的游戏对象将显示为暗色。
		  3. 单击游戏对象旁边的小眼睛图标可手动切换其活动状态。
		  4. 可以在层级视图中，以树状结构方式处理场景中的游戏对象及其子对象的活动状态。
		  
		  
		  请注意，使用`SetActive()`方法可以在运行时动态更改游戏对象的活动状态，而`activeSelf`和`activeInHierarchy`属性则用于检查游戏对象的当前活动状态。在层级视图中的操作主要用于静态调整游戏对象的活动状态，以便在编辑器中检查和调整场景的结构。
		  
		- Destroy()

		  在Unity中，可以使用`Destroy()`函数来删除游戏对象和组件。`Destroy()`方法用于立即删除游戏对象或组件，以从场景或层级中移除它们。
		  
		  使用`Destroy()`函数删除游戏对象：
		  - 若要删除一个游戏对象，可以直接调用`Destroy()`方法并传递要删除的游戏对象作为参数。
		  - 例如，使用以下代码可以删除名为`gameObjectToRemove`的游戏对象：
		     ```csharp
		     Destroy(gameObjectToRemove);
		     ```
		  
		  使用`Destroy()`函数删除组件：
		  - 若要删除组件，可以通过访问具有该组件的游戏对象，然后调用`Destroy()`方法来删除组件。
		  - 例如，使用以下代码可以删除名为`componentToRemove`的组件：
		     ```csharp
		     Destroy(componentToRemove);
		     ```
		  请注意，删除游戏对象或组件将在下一帧开始时生效，因为要在正确的时间点完成销毁操作。在`Destroy()`方法之后的代码将被执行，但是删除的游戏对象或组件将在下一帧被移除。因此，在删除游戏对象或组件后，最好采取一些预防措施以避免可能的错误或异常。
		  
		  另外，还有一些其他相关的方法可以使用：
		  - `DestroyImmediate()`方法可以在同一帧中立即删除游戏对象或组件，而不需要等待下一帧。
		  - `DestroyObject()`方法用于从场景中删除游戏对象，并在下一帧开始时销毁它。
		  - `DestroyObjectImmediate()`方法用于立即从场景中删除游戏对象。
		  
		  请根据具体情况选择合适的方法来删除游戏对象或组件。使用这些函数时要小心，确保删除正确的对象和组件，并避免可能的内存泄漏。
		  
	- 组件移动

		- Translate 和 Rotate

		  在Unity中，可以使用`Translate()`和`Rotate()`方法来更改非刚体对象的位置和旋转。这些方法是Transform组件的成员函数，可以直接应用于非刚体对象的Transform组件。
		  
		  使用Translate更改位置：
		  - `Translate()`方法可以将对象移动到新的位置。它接受一个参数`translation`，表示要移动的距离，可以是一个Vector3类型的值，也可以是三个分量的XYZ坐标。
		  - 例如，使用以下代码将非刚体对象`transform`沿着向量(1, 0, 0)移动1个单位的距离：
		     ```csharp
		     transform.Translate(Vector3.right);
		     ```
		     或者，使用以下代码将对象沿着局部坐标系的X轴移动1个单位的距离：
		     ```csharp
		     transform.Translate(1f, 0f, 0f, Space.Self);
		     ```
		  
		  使用Rotate更改旋转：
		  - `Rotate()`方法可以将对象旋转到新的方向。它接受一个参数`eulerAngles`，表示要旋转的欧拉角（以度为单位），可以是一个Vector3类型的值，也可以是三个分量的XYZ轴旋转角度。
		  - 例如，使用以下代码将非刚体对象`transform`绕向量(0, 1, 0)旋转90度：
		     ```csharp
		     transform.Rotate(Vector3.up * 90f);
		     ```
		     或者，使用以下代码将对象绕局部坐标系的Y轴旋转90度：
		     ```csharp
		     transform.Rotate(0f, 90f, 0f, Space.Self);
		     ```
		  请注意，`Translate()`和`Rotate()`方法将在下一帧开始时应用变换，因此在调用后的代码可能会在变换之前执行。如果需要在变换之后立即执行某些操作，可以使用协程、回调函数或其他适当的方法。
		  
		  此外，还可以使用`transform.position`和`transform.rotation`属性直接设置非刚体对象的位置和旋转。例如，`transform.position = newPosition`将直接更改对象的位置为`newPosition`，`transform.rotation = newRotation`将直接更改对象的旋转为`newRotation`。
		  
		  请根据具体的需求选择适合的方法来更改非刚体对象的位置和旋转。记得在更改对象位置和旋转之前，在代码中应该将对象的Transform组件引用赋值给变量`transform`。
		  
		- getButton和getKey

		  在Unity项目中，可以通过Unity Input System获取和处理用于输入的按钮或键以及轴。
		  
		  1. 获取按钮或键的输入：
		     - 使用`Input.GetButtonDown("ButtonName")`来检测按下按钮或键。其中，"ButtonName"是按钮或键的名称。
		     - 使用`Input.GetButtonUp("ButtonName")`来检测释放按钮或键。
		     - 使用`Input.GetButton("ButtonName")`来检测按钮或键是否一直按住。
		     - 例如，使用以下代码检测鼠标左键被按下：
		       ```csharp
		       if (Input.GetButtonDown("Fire1"))
		       {
		           // 执行相应的操作
		       }
		       ```
		  
		  2. 获取轴的输入：
		     - 使用`Input.GetAxis("AxisName")`来获取轴的输入值。其中，"AxisName"是轴的名称。
		     - 输入值通常在-1到1之间，表示轴的位置。
		     - 例如，使用以下代码获取水平轴的输入：
		       ```csharp
		       float horizontalInput = Input.GetAxis("Horizontal");
		       ```
		  
		  如果想要修改按钮或键的行为，可以使用Unity的Input Manager进行配置：
		  
		  1. 打开Unity编辑器，点击`Edit`菜单，选择`Project Settings`，然后选择`Input`。
		  2. 在Inspector视图中，可以看到现有的按钮和轴。
		  3. 可以修改按钮和轴的名称、正值按键、负值按键、响应速度等属性。
		  4. 若要添加新的按钮或轴，请点击面板右上角的加号按钮，然后在名称字段中输入新的名称，并按需配置其他属性。
		  
		  在代码中使用`Input.GetButton()`、`Input.GetButtonDown()`、`Input.GetButtonUp()`和`Input.GetAxis()`时，将使用Input Manager中配置的按钮和轴的名称来检测和获取输入。
		  
		  使用Unity Input System和Input Manager，可以轻松地获取和修改游戏对象的按钮、键和轴的输入，使用户能够与游戏进行交互。
		  
		- GetAxis

		  在Unity中，可以通过以下步骤获取基于轴的输入，并使用Unity的Input Manager进行修改：
		  
		  1. 获取基于轴的输入：
		     - 使用`Input.GetAxis("AxisName")`来获取轴的输入值。其中，"AxisName"是轴的名称。
		     - 轴的输入值范围通常在-1到1之间，表示轴的位置。
		     - 例如，使用以下代码获取水平轴的输入：
		       ```csharp
		       float horizontalInput = Input.GetAxis("Horizontal");
		       ```
		  
		  2. 修改轴的输入：
		     - 打开Unity编辑器，点击`Edit`菜单，选择`Project Settings`，然后选择`Input`。
		     - 在Inspector视图中，可以看到已配置的按钮和轴。
		     - 找到要修改的轴，可以更改其名称、正值和负值按钮、响应速度等属性。
		     - 可以通过点击轴上的下拉箭头来选择新的正值和负值按钮。
		     - 若要添加新的轴，请点击面板右上角的加号按钮，在名称字段中输入新的名称，并按需配置其他属性。
		  
		  通过使用`Input.GetAxis()`获取轴的输入时，会使用Input Manager中配置的轴的名称来检测和获取输入。
		  
		  使用Unity Input System和Input Manager，可以轻松地获取和修改游戏对象的基于轴的输入，以及配置和自定义游戏的输入设置。
		  
		- LookAt

		  使用 LookAt 函数使一个游戏对象的变换组件面向另一个游戏对象的变换组件
		  
		  public class CameraLookAt : MonoBehaviour
		  {
		      public Transform target;
		      void Update ()
		      {
		          transform.LookAt(target);
		      }
		  }
		  
		- DeltaTime

		  DeltaTime（Δt）是一个指示每帧持续时间的概念，通常以秒为单位。在游戏中，帧速率（FPS）可能会变化，因此使用 Delta Time 可以使游戏中的动画、物理模拟和其他时间相关的操作按比例进行计算，以实现平滑的动画和一致的行为。
		  
		  在每一帧更新中，Delta Time 描述了上一帧的持续时间，它可以用于以下几方面：
		  
		  1. 动画：使用 Delta Time 将每个帧的动画变化与时间无关，而是与帧速率相关联，从而在不同帧速率的情况下保持一致的动画播放速度。
		  
		  2. 运动和移动：将 Delta Time 与对象的速度相乘，可以确定对象在一帧中应该移动的距离，从而在不同帧速率下保持一致的移动速度。
		  
		     ```csharp
		     void Update()
		     {
		         transform.Translate(Vector3.up * moveSpeed * Time.deltaTime);
		     }
		     ```
		  
		  3. 物理模拟：许多游戏引擎使用物理引擎进行物体的模拟。在物理模拟中，将 Delta Time 用于应用力、速度和加速度等参数的计算，以确保物理效果在不同帧速率下的表现一致。
		  
		  4. 操作延迟和平滑：通过将 Delta Time 乘以一个系数（例如，0.1）并将其与输入或值进行插值，可以实现平滑过渡，从而减少突然的变化和操作的延迟。
		  
		     ```csharp
		     float smoothedValue = Mathf.Lerp(currentValue, targetValue, smoothness * Time.deltaTime);
		     ```
		  
		  综上所述，Delta Time 是一个重要的概念，可以用于在游戏中处理时间相关的操作，以确保在不同帧速率下保持一致的行为和平滑的动画效果。它通过将帧的持续时间考虑在内，使得游戏在不同的计算机和不同的帧速率下具备良好的表现。
		  
### Markdown基本语法

- 概念

  Markdown是一种纯文本格式的标记语言。通过简单的标记语法，它可以使普通文本内容具有一定的格式。
  
	- 优点

	  1、因为是纯文本，所以只要支持Markdown的地方都能获得一样的编辑效果，可以让作者摆脱排版的困扰，专心写作。
	   2、操作简单。比如:WYSIWYG编辑时标记个标题，先选中内容，再点击导航栏的标题按钮，选择几级标题。要三个步骤。而Markdown只需要在标题内容前加#即可
	  
	- 缺点

	  1、需要记一些语法（当然，是很简单。五分钟学会）。
	  2、有些平台不支持Markdown编辑模式。
	  
- 内容

	- 标题

	  在想要设置为标题的文字前面加#来表示
	   一个#是一级标题，二个#是二级标题，以此类推。支持六级标题。
	  注：标准语法一般在#后跟个空格再写文字，貌似简书不加空格也行。示例：
	  # 这是一级标题
	  ## 这是二级标题
	  ### 这是三级标题
	  #### 这是四级标题
	  ##### 这是五级标题
	  ###### 这是六级标题
	  
	- 字体

	  加粗：要加粗的文字左右分别用两个*号包起来
	  斜体：要倾斜的文字左右分别用一个*号包起来
	  斜体加粗：要倾斜和加粗的文字左右分别用三个*号包起来
	  删除线：要加删除线的文字左右分别用两个~~号包起来
	  示例：
	  **这是加粗的文字**
	  *这是倾斜的文字*`
	  ***这是斜体加粗的文字***
	  ~~这是加删除线的文字~~
	  
	- 引用

	  在引用的文字前加>即可。引用也可以嵌套，如加两个>>三个>>>
	  
	- 分割线

	  三个或者三个以上的 - 或者 * 都可以。
	  示例：
	  ---
	  ----
	  ***
	  *****
	  
	- 图片

	  语法：
	  ![图片alt](图片地址 ''图片title'')
	  图片alt就是显示在图片下面的文字，相当于对图片内容的解释。
	  图片title是图片的标题，当鼠标移到图片上时显示的内容。title可加可不加
	  示例：
	  ![blockchain](https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/
	  u=702257389,1274025419&fm=27&gp=0.jpg "区块链")
	  
	  markdown格式追求的是简单、多平台统一。那么图片的存储就是一个问题，需要用图床，提供统一的外链，这样就不用在不同的平台去处理图片的问题了。才能做到书写一次，各处使用。
	  
	- 超链接

	  语法：
	  [超链接名](超链接地址 "超链接title")
	  title可加可不加
	  示例：
	  [简书](http://jianshu.com)
	  [百度](http://baidu.com)
	  注：Markdown本身语法不支持链接在新页面中打开，貌似简书做了处理，是可以的。别的平台可能就不行了，如果想要在新页面中打开的话可以用html语言的a标签代替。
	  <a href="超链接地址" target="_blank">超链接名</a>
	  示例
	  <a href="https://www.jianshu.com/u/1f5ac0cf6a8b" target="_blank">简书</a>
	  
	- 列表

		- 无序列表

		  语法：
		  无序列表用 - + * 任何一种都可以
		  - 列表内容
		  + 列表内容
		  * 列表内容
		  注意：- + * 跟内容之间都要有一个空格
		  
		- 有序列表

		  语法：
		  数字加点
		  1. 列表内容
		  2. 列表内容
		  3. 列表内容
		  注意：序号跟内容之间要有空格
		  
		- 列表嵌套

		  上一级和下一级之间敲三个空格即可
		  
		  一级无序列表内容
		  
		  二级无序列表内容
		  二级无序列表内容
		  二级无序列表内容
		  一级无序列表内容
		  
		  二级有序列表内容
		  二级有序列表内容
		  二级有序列表内容
		  一级有序列表内容
		  
		  二级无序列表内容
		  二级无序列表内容
		  二级无序列表内容
		  一级有序列表内容
		  
		  二级有序列表内容
		  二级有序列表内容
		  二级有序列表内容
		  
	- 表格

	  语法：
	  表头|表头|表头
	  ---|:--:|---:
	  内容|内容|内容
	  内容|内容|内容
	  
	  第二行分割表头和内容。
	  - 有一个就行，为了对齐，多加了几个
	  文字默认居左
	  -两边加：表示文字居中
	  -右边加：表示文字居右
	  注：原生的语法两边都要用 | 包起来。此处省略
	  
	  示例：
	  姓名|技能|排行
	  --|:--:|--:
	  刘备|哭|大哥
	  关羽|打|二哥
	  张飞|骂|三弟
	  
	- 代码

	  语法：
	   单行代码：代码之间分别用一个反引号包起来
	  `代码内容`
	  代码块：代码之间分别用三个反引号包起来，且两边的反引号单独占一行
	  (```)
	    代码...
	    代码...
	    代码...
	  (```)
	  注：为了防止转译，前后三个反引号处加了小括号，实际是没有的。这里只是用来演示，实际中去掉两边小括号即可。
	  
	  示例：
	  单行代码
	  `create database hero;`
	  代码块
	  (```)
	      function fun(){
	           echo "这是一句非常牛逼的代码";
	      }
	      fun();
	  (```)
	  
	- 流程图

	  ```flow
	  st=>start: 开始
	  op=>operation: My Operation
	  cond=>condition: Yes or No?
	  e=>end
	  st->op->cond
	  cond(yes)->e
	  cond(no)->op
	  &```
	  
### Unity游戏开发中的脚本设计
- Unity中不同脚本间的交互

	- 方法一

	  通过在编辑器里面拖动，来持有这个对象去调用对应的函数，此方法比较简单。
	  在编辑器中新建2个脚本。
	  public class Ascript : MonoBehaviour {
	      public int value = 1; //Ascript类内部变量
	      public void DoSomething()
	      {
	          Debug.Log("Ascript doing!"); //在Unity控制台中显示"Ascript doing!"
	      }
	  }
	  我们想用Main脚本去调用Ascript脚本。我们就在Main脚本中声明一个Ascript脚本的对象。
	  public Ascript ascript;
	  
	  
	  这样在代码编写的时候已经可以调用A对象中的任何 public 变量和函数(公开出去的成员才能被外部类调用)。
	  现在在Main脚本中有如下内容：
	  public class Main : MonoBehaviour {
	      public Ascript ascript;
	      private int Mvalue;
	      public void DoASomething()
	      {   
	          //ascript.DoSomething(); 此时若直接这样运行，将报错，因为此时ascript为空引用,程序并不知道是哪个脚本。
	          if(ascript != null) //加上一个判断，使程序更安全，如果为空了，就不执行此代码。
	          {
	              Mvalue = ascript.value; //Mvalue = 1;
	              ascript.DoSomething(); //输出 Ascript doing!
	          }
	      }
	      void Start()
	      {
	          DoASomething(); //游戏开始时调用
	      }
	  }
	  
	  
	  现在我们要对它赋值,这个时候我们在编辑器拖一个有Ascript脚本的实体对象给Main脚本的ascript就可以了。
	  
	  
	- 方法二

	  直接使用SendMessage()方法,可在Unity API中查看此方法，此方法比较简单。
	  由于SendMessage()方法已不被新版本Unity推荐，故此方法只需了解，不推荐使用。
	  
	  
	- 方法三

	  现在我们将Ascript脚本的DoSomething()函数改成:
	  public class Ascript : MonoBehaviour {
	      public int value = 1; //Ascript类内部变量
	      public static void DoSomething() //静态方法
	      {
	          Debug.Log("Ascript doing!"); //在Unity控制台中显示"Ascript doing!"
	      }
	  }
	  
	  可以发现一个新的前缀 static 被放到了DoSomething()方法前
	  static 表示静态
	  关于静态类和静态类成员 可以查看C#官方文档中的介绍静态类和静态类成员(C# 编程指南)
	  现在在Main脚本中我们就可以直接使用 Ascript.DoSomething(); 调用：
	  public class Main : MonoBehaviour {
	      //public Ascript ascript; //不再使用这个方式获取ascript引用
	      private int Mvalue;
	      public void DoASomething()
	      {   
	          //Mvalue = Ascript.value; 调用Ascript的变量会报错，因为此变量不是静态变量
	          Ascript.DoSomething(); //直接调用静态方法 输出 Ascript doing!
	      }
	      void Start()
	      {
	          DoASomething(); //游戏开始时调用
	      }
	  }
	  
	  
	  此时你就会想如果想要Ascript.value也可以被Main调用，需要怎么样呢？
	  public static int value; //Ascript类内部静态变量
	  答案显而易见，只需要将Ascript的value变量定义为静态变量即可使上方被注释的代码正常运行
	  同理，如果想将整个Ascript内部的所有方法或者变量全都允许被其他类调用，可以直接定义此类为静态类
	  但是静态虽然方便调用，但是它本身是反设计模式的，违反OOP思想，缺乏扩展性和可测试性，兼容性差。而且在类装载的时候被装载到内存，不自动进行摧毁，会一直存在内存中，所以除非一些非常特殊的类如Global,尽可能避免静态类
	  
	  
- 单例设计模式

  那么有没有一种方式能像静态类一样方便调用，又能效率比静态类高且符合设计模式呢？
  现在让我们来探讨一些更有趣的方法
  我们在在上面的基础上改成如下这个样子。
  public class Ascript : MonoBehaviour {
      public static Ascript Instance;
      public int value = 1;
      void Start() 
      {
          Instance = this;
      }
      public void DoSomething()
      {
          Debug.Log("Ascript doing!");
      }
  }
  
  
  我们把Main脚本中的调用改成：Ascript.Instance.DoSomething();
  public class Main : MonoBehaviour {
      //public Ascript ascript; 无需再引用ascript 
      private int Mvalue;
      public void DoASomething()
      {   
          //Ascript.DoSomething(); 不再使用这种方式
          Ascript.Instance.DoSomething(); //输出 Ascript doing!
          Mvalue = Ascript.Instance.value; // Mvalue = 1;
          
      }
      void Start()
      {
          DoASomething(); //游戏开始时调用
      }
  }
  
  
  
  注意：我们这个时候Main脚本已经不持有Ascript这个对象了。但是场景一定要这个对象，如果没有的话会报错。如果我们场景里面有很多这个对象，他会找到这个对象最早生成的那个，注意不是你创建的实体对象而是第一个拖上这个脚本的对象。
  
  
  下面将此方法推广，使得即使不继承于MonoBehaviour的类也可以让其他脚本直接调用(即利用静态构造函数替代Start()方法),称此方法为单例设计模式
  
  public class Singleton 
  {
      public static Singleton instance;
      public static Singleton Instance
      {
          get {
              if (instance==null)
              {
                  instance = new Singleton();
              }
              return instance;
          }
      }
  }
  //在另一个类中使用 Singleton.Instance. 就可以调用Singleton内部的方法或者变量
  
  
  此处为最基础的单例，但实际上是线程不安全的，后续仍有优化空间，此处只为了理解单例模式，故以此举例。
  单例模式是软件工程学中最富盛名的设计模式之一，在开发过程中十分常见，所以我们经常会使用 泛型 写一个单例模式的基类，这样我们就可以通过继承该基类轻松实现单例模式，并且不会随着场景切换而销毁，代码如下所示：
  ///<summary>
  /// 单例基类
  ///<summary>
  public class Singleton<T> : MonoBehaviour where T : Singleton<T>
  {
      public static T Instance { get; private set; } //属性
      protected void Awake()
      {
          if (Instance == null)
          {
              Instance = (T) this;
              DontDestroyOnLoad(gameObject); //该实例不会随场景切换而销毁
          }
          else
          {
              Destroy(gameObject); //消除重复实例
          }
      }
  }
  ///<summary>
  /// 游戏核心管理脚本
  ///<summary>
  public class Manager : Singleton<GameManager> //继承于单例类的Manager
  {
      public int Value = 0;
  }
  //在另一个类中使用 Manager.Instance. 就可以调用Manager内部的成员
  //此处为 Manager.Instance.Value，即可改变此参数值或获取值。
  
  
  方法总结
  
  第一种利用脚本互相的挂载，试想想，如果A的参数需要其他多个脚本B C D E 都能获取，那么用第一种方法，你需要让BCDE都引用A才可以，如果是10个类，20个类呢？每个都需要引用岂不是很麻烦？ 到最后你自己都不想维护了，所以单例的重要性不言而喻，
  
  第二种方法已弃用
  
  第三种利用static静态成员直接调用, 但必须要清楚的是我们应该尽量避免使用静态变量
  
  在Unity中，由于总是可以用各种方法找到一个对象，所以静态变量想不用，总是可以不用。比如你在根节点创建一个名为GameMode的GameObject，那么想用静态变量的地方，都可以改成非静态的扔到GameMode里面。访问的时候先找到唯一的那个GameObject对象再访问变量，用起来和静态变量区别不大。
  再说关键的“对象生命周期”的问题，静态变量可以用类名直接访问，写起来很方便，比如如果游戏客户端只有唯一一个玩家对象，类型为class Player，那么Player的血量就可以设计成直接用：Player.Hp 来访问。
  这样写很多时候没问题，但是严格来说，必须注意：Player.Hp在什么时候开始可用，什么时候失效？由于Player对象肯定是在某个时刻创建，某个时刻销毁的（最晚是在游戏结束时销毁）。那么在Player创建之前、结束之后，Player.Hp是不可访问的，不应该被访问。这就是带来一个隐患：作为静态变量，Player.Hp可以随时访问，大不了读出来是0，但是原则上来讲，Player对象没有创建好的时候，Hp是不存在的。
  游戏中的绝大部分物体都有这个问题，因为基本上，场景中所有对象都有着出生、死亡的时刻，包括各种管理器对象，用static静态变量，则它的语法与事实会存在出入。（因为static静态变量是绑定在类上，从逻辑上看，类比任何对象出现都早，结束都晚。哪怕一个对象都没有的时候，也已经有类了。）
  这个问题在什么时候变得明显不对呢？就是不同类型的对象之间有相互依赖的时候。比如UI界面用到了任务管理器对象，Player用到了UI对象，任务管理器又在某些时候会访问Player的数据。这时候用静态变量很难理清哪个对象在什么时候能用、什么时候不能用。虽然这些对象大部分时候都不销毁，但未来项目变化的时候，东一个西一个的静态变量，就可能变成滋生BUG的温床。
  
  于是乎今天的主角就要登场了，使用 单例设计模式，单例有一个非常大的好处：它把以上讨论的，访问某种唯一对象的模式规范化了。规范化就意味着统一、好查。如果搞错了生命期，发现某个管理器找不到了，你就可以到创建、销毁的地方去查它，很容易就发现设计上的漏洞。当游戏中的某一个游戏对象永远只有一个实例的时候，那么就可以使用单例模式。
  
  由于单例模式在内存中只有一个实例，减少内存开支，特别是一个对象需要频繁地创建销毁时，而且创建或销毁时性能又无法优化,单例模式就非常明显了
  由于单例模式只生成一个实例，所以，减少系统的性能开销，当一个对象产生需要比较多的资源时，如读取配置，产生其他依赖对象时，则可以通过在应用启动时直接产生一个单例对象，然后永久驻留内存的方式来解决。
  单例模式可以避免对资源的多重占用，例如一个写文件操作，由于只有一个实例存在内存中，避免对同一个资源文件的同时写操作
  单例模式可以在系统设置全局的访问点，优化和共享资源访问，例如，可以设计一个单例类，负责所有数据表的映射处理。
  
  当然单例也并不是完美的：
  
  单例模式一般没有接口，扩展很困难，若要扩展，除了修改代码基本上没有第二种途径可以实现。
  单例对象如果持有Context，那么很容易引发内存泄漏，此时需要注意传递给单例对象的Context最好是Application Context。
  
  当然每种方法有每种方法使用的地方，不代表一成不变，所以要根据实际运用，选择合适的方法。
  
  
  
- 关于面向对象编程（继承）

  
  什么是继承？
  
  继承是面向对象程序设计中最重要的概念之一。
  借助继承，我们能够定义多个 可重用、扩展或修改父类行为 的子类。
  已有的一个类被称为基类(父类)，而新创建的并继承于该父类的一些类被称为派生类(子类)。
  一个父类可以有多个子类，一个子类只能有一个父类，但一个子类可以通过接口的方式实现多重继承。
  如果想了解接口，可以查阅Interface C#官方文档
  为什么要用继承？
  继承允许我们根据一个类来定义另一个类，这使得创建和维护应用程序变得更容易。同时也有利于重用代码和节省开发时间。当创建一个类时，程序员不需要完全重新编写新的数据成员和成员函数，只需要设计一个新的类，继承了已有的类的成员即可。
  继承如何在Unity中体现？
  接下来用大家已经做过的roll a ball举例说明，我们想设计小球吃方块获得相应buff，如果有多种方块，例如加Hp的方块、减Hp的方块、增加速度的方块等等，我们现在打算对每一种方块挂载一个脚本。分别命名为ChangeHpBuff,ChangeSpeedBuff...可能的实现如下：
  ///<summary>
  /// Player脚本
  ///<summary>
  public class Player
  {
      public float Hp;
      public float Speed;
      //.....等等玩家自身属性
      public void move()
      {
          //处理玩家移动的代码块
      }
  }
  ///<summary>
  /// 加血Buff脚本
  ///<summary>
  public class ChangeHpBuff: MonoBehaviour {
      public GameObject player; //声明玩家对象
      public float LastingTime;//声明Buff持续时间
      public float DeltaHp;//声明Buff增加血量
      public BuffEffect()//该Buff的效果处理函数
      {
          player.GetComponent<Player>().Hp+=DeltaHp; //获取Player对象里的Player脚本组件 对其成员Hp进行增加
      }
      void OnTriggerEnter(Collision other)
      {
          if(other.gameObject.CompareTag("Player"))
          {
              BuffEffect();
              Destroy(gameObject);
          }
      }   
      //......
  }
  ///<summary>
  /// 加速Buff脚本
  ///<summary>
  public class ChangeSpeedBuff: MonoBehaviour {
      public GameObject player;//声明玩家对象
      public float LastingTime;//声明Buff持续时间
      public float DeltaSpeed;//声明Buff增加速度
      public BuffEffect()//该Buff的效果处理函数
      {
          player.GetComponent<Player>().Speed+=DeltaSpeed;//获取Player对象里的Player脚本组件 对其成员Speed进行增加
      }
      void OnTriggerEnter(Collision other)
      {
          if(other.gameObject.CompareTag("Player"))
          {
              BuffEffect();
              Destroy(gameObject);
          }
      }
      //......
  }
  
  
  可以看到代码里每一种Buff脚本都需要重复引用player,LastingTime等等，那么这些重复的功能(代码)，虽然复制粘贴很方便，但是这实在是太繁琐了(不够优雅)，并且代码过于重复，不利于后期维护查阅。于是我们便可以通过继承去优化结构，节省大量时间。
  这里要提醒大家，下面的内容可能过多的新关键词，不用着急，会慢慢跟大家解释意思。
  ///<summary>
  ///Buff基类 场景中不需要挂载
  ///<summary>
  public abstract class Buff //定义抽象基类Buff
  {
      public enum BuffKind //定义枚举类型 Buff种类
      {
          HpBuff, //回血Buff
          SpeedBuff,//加速Buff
      }
      public float m_Length;//Buff持续时间
      public BuffKind m_BuffKind;//Buff的类型
      public Player m_Player;//作用的实体
      public Buff(Player player, BuffKind buffKind, float length)//构造函数传参 
      {
          m_Player = player; //第一个参数表示作用的实体 本例子中只有玩家 所以命名为Player 其实应该命名为实体
          m_BuffKind = buffKind; //第二个参数表示作用Buff的种类
          m_Length = length; //第三个表示该Buff持续的时间
      }
      public virtual void OnAdd() { }//添加Buff的虚函数
      //public virtual void OnRemove(){} 可以自行思考如何写Buff移除功能
  }
  
  
  关于 abstract 即修饰为抽象类型
  具体资料可查阅 abstract C#官方文档
  关于 enum 即枚举类
  具体资料可查阅 enum C#官方文档
  关于构造函数 即在为新对象分配内存之后，new 运算符立即调用构造函数。
  具体资料可查阅 构造函数 C#官方文档
  关于 virtual 即被它修饰的成员，需要使它们可以在派生类中被重写
  具体资料可查阅 virtual C#官方文档
  ///<summary>
  ///一种Buff类此处为加速Buff 场景中不需要挂载
  ///<summary>
  public class SpeedBuff : Buff //继承于Buff类 而不是默认的 MonoBehaviour 类
  {
      public float DeltaSpeed = 10f; //增加的速度
      public SpeedBuff(Player player, BuffKind buffKind, float length) : base(player, buffKind, length) { } //构造函数传参
      public override void OnAdd() //重写父类OnAdd()函数
      {
          base.OnAdd(); 
          m_Player.Speed += DeltaSpeed; //增加玩家对象的Speed
      }
  }
  
  
  关于 override 即扩展或修改
  具体资料可查阅 override C#官方文档
  public class HpBuff: Buff //继承于Buff类 而不是默认的 MonoBehaviour 类
  {
      //思考HpBuff类该怎么写，可以参考上方的SpeedBuff，自己尝试写写并是否能在游戏中运行
  }
  
  
  现在Buff的管理已经完成了，可以看到Buff的基类包含了每个Buff都需要作用的
  1.作用的对象Player-Player
  2.作用的Buff种类-BuffKind
  3.作用的时长-Length
  4.添加Buff的方法-OnAdd()
  而不需要在每个Buff类中都写，避免了重复，在每个Buff类中现在只需要定义该Buff自身的一些效果，利用构造函数传递参数，重写一下添加Buff时调用的函数OnAdd()即可。
  那么现在该如何给玩家添加Buff呢？请看下方代码：
  public class Player : MonoBehaviour
  {
      public float Speed; //移动速度
      public float Hp; //玩家血量
      //....刚体，移动等省略
      public void AddBuff(Buff buff) //定义一个添加Buff的内部函数 参数为Buff类型
      {
          buff.OnAdd();
      }
      void OnTriggerEnter(Collider other)
      {
          if (other.gameObject.CompareTag("SpeedBuff")) //当碰到标签为 SpeedBuff 的触发对象
          {
              //....
              AddBuff(new SpeedBuff(this, Buff.BuffKind.SpeedBuff, 10f));
              ///<summary>        
              ///添加一个 SpeedBuff 作用
              ///实体为Player(this指这里的Player)      
              ///作用类型为Buff类里的枚举类型SpeedBuff       
              ///Buff持续时间为10秒       
              ///<summary>        
              //....
          }
      }
  }
  
  
  当然为了给大家一些帮助，可以看到Buff基类中定义了一个Buff持续时间，但是只有添加Buff(OnAdd())的相关功能，并没有移除Buff(OnRemove())的相关功能，就留给大家来做吧。
  扩展问题：如果想要能显示玩家此时身上拥有哪些Buff，该如何实现此功能？
  对传入的Buff持续时间进行处理当时间到时，执行Buff移除功能的函数，相信你可以做到的。
  总结
  通常情况下，继承用于表示基类和一个或多个派生类之间的“is a”关系，其中派生类是基类的特定版本；派生类是基类的具体类型。 例如，Publication 类表示任何类型的出版物，Book 和 Magazine 类表示出版物的具体类型。请注意，“is a”还表示类型与其特定实例化之间的关系。 在以下示例中，Automobile 类包含三个唯一只读属性：Make（汽车制造商）、Model（汽车型号）和 Year（汽车出厂年份）。 Automobile 类还有一个自变量被分配给属性值的构造函数，并将 Object.ToString 方法重写为生成唯一标识 Automobile 实例（而不是 Automobile 类）的字符串。基于继承的“is a”关系最适用于基类和向基类添加附加成员或需要基类没有的其他功能的派生类。
  
## Git与Github的使用方法与相关语法

### Git简介

- 集中式和分布式

  Linus一直痛恨的CVS及SVN都是集中式的版本控制系统，而Git是分布式版本控制系统，集中式和分布式版本控制系统有什么区别呢？
  
  集中式版本控制系统，版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。
  ￼
  
  集中式版本控制系统最大的缺点就是必须联网才能工作
  
  分布式版本控制系统与集中式版本控制系统不同。首先，分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。
  
  和集中式版本控制系统相比，分布式版本控制系统的安全性要高很多，因为每个人电脑里都有完整的版本库，某一个人的电脑坏掉了不要紧，随便从其他人那里复制一个就可以了。而集中式版本控制系统的中央服务器要是出了问题，所有人都没法干活了。
  
  在实际使用分布式版本控制系统的时候，其实很少在两人之间的电脑上推送版本库的修改，因为可能你们俩不在一个局域网内，两台电脑互相访问不了，也可能今天你的同事病了，他的电脑压根没有开机。因此，分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已。
  
  CVS作为最早的开源而且免费的集中式版本控制系统，直到现在还有不少人在用。由于CVS自身设计的问题，会造成提交文件不完整，版本库莫名其妙损坏的情况。同样是开源而且免费的SVN修正了CVS的一些稳定性问题，是目前用得最多的集中式版本库控制系统。
  
  分布式版本控制系统除了Git以及促使Git诞生的BitKeeper外，还有类似Git的Mercurial和Bazaar等。这些分布式版本控制系统各有特点，但最快、最简单也最流行的依然是Git！
  
- 安装Git

	- 在Linux上安装Git

	  首先，你可以试着输入git，看看系统有没有安装Git：
	  $ git
	  The program 'git' is currently not installed. You can install it by typing:
	  sudo apt-get install git
	  
	  像上面的命令，有很多Linux会友好地告诉你Git没有安装，还会告诉你如何安装Git。
	  
	  如果你碰巧用Debian或Ubuntu Linux，通过一条sudo apt-get install git就可以直接完成Git的安装，非常简单。
	  
	  老一点的Debian或Ubuntu Linux，要把命令改为sudo apt-get install git-core，因为以前有个软件也叫GIT（GNU Interactive Tools），结果Git就只能叫git-core了。由于Git名气实在太大，后来就把GNU Interactive Tools改成gnuit，git-core正式改为git。
	  
	  如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入：./config，make，sudo make install这几个命令安装就好了。
	  
	- 在Mac OS X上安装Git

	  有两种安装Git的方法。
	  
	  一是安装homebrew，然后通过homebrew安装Git，具体方法请参考homebrew的文档：http://brew.sh/。
	  
	  第二种方法更简单，也是推荐的方法，就是直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。
	  
	  Xcode是Apple官方IDE，功能非常强大，是开发Mac和iOS App的必选装备，而且是免费的！
	  
	- 在Windows上安装Git

	  在Windows上使用Git，可以从Git官网直接下载安装程序，然后按默认选项安装即可。
	  
	  安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！
	  
	  安装完成后，还需要最后一步设置，在命令行输入：
	  $ git config --global user.name "Your Name"
	  $ git config --global user.email "email@example.com"
	  
	  因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。
	  
### 仓库管理

- 创建版本库

  版本库又名仓库，英文名repository，可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。
  
  首先，选择一个合适的地方，创建一个空目录：
  $ mkdir learngit
  $ cd learngit
  $ pwd
  /Users/michael/learngit
  pwd命令用于显示当前目录。如果使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。
  
  第二步，通过git init命令把这个目录变成Git可以管理的仓库：
  $ git init
  Initialized empty Git repository in /Users/michael/learngit/.git/
  瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以看见。
  
  第三步，把文件添加到版本库
  首先这里再明确一下，所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。
  不幸的是，Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的，前面我们举的例子只是为了演示，如果要真正使用版本控制系统，就要以纯文本方式编写文件。因为文本是有编码的，比如中文有常用的GBK编码，日文有Shift_JIS编码，如果没有历史遗留问题，强烈建议使用标准的UTF-8编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。
  
  疑难解答：
  Q：输入git add readme.txt，得到错误：fatal: not a git repository (or any of the parent directories)。
  A：Git命令必须在Git仓库目录内执行（git init除外），在仓库目录外执行是没有意义的。
  Q：输入git add readme.txt，得到错误fatal: pathspec 'readme.txt' did not match any files。
  A：添加某个文件时，该文件必须在当前目录下存在，用ls或者dir命令查看当前目录的文件，看看文件是否存在，或者是否写错了文件名。
  
  小结：
  初始化一个Git仓库，使用git init命令。
  添加文件到Git仓库，分两步：
  使用命令git add <file>，注意，可反复多次使用，添加多个文件；
  使用命令git commit -m <message>，完成。
  
- 把文件添加到版本库

  使用Windows的童鞋要特别注意：
  千万不要使用Windows自带的记事本编辑任何文本文件。原因是Microsoft开发记事本的团队使用了一个非常弱智的行为来保存UTF-8编码的文件，他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符，你会遇到很多不可思议的问题，比如，网页第一行可能会显示一个“?”，明明正确的程序一编译就报语法错误，等等，都是由记事本的弱智行为带来的。建议下载Visual Studio Code代替记事本，不但功能强大，而且免费！
  
  言归正传，现在我们编写一个readme.txt文件，内容如下：
  Git is a version control system.
  Git is free software.
  一定要放到learngit目录下（子目录也行），因为这是一个Git仓库，放到其他地方Git再厉害也找不到这个文件。
  
  和把大象放到冰箱需要3步相比，把一个文件放到Git仓库只需要两步。
  第一步，用命令git add告诉Git，把文件添加到仓库：
  $ git add readme.txt
  执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。
  第二步，用命令git commit告诉Git，把文件提交到仓库：
  $ git commit -m "wrote a readme file"
  [master (root-commit) eaadf4e] wrote a readme file
   1 file changed, 2 insertions(+)
   create mode 100644 readme.txt
  
  简单解释一下git commit命令，-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。
  
  嫌麻烦不想输入-m "xxx"行不行？确实有办法可以这么干，但是强烈不建议你这么干，因为输入说明对自己对别人阅读都很重要。实在不想输入说明的童鞋请自行Google，我不告诉你这个参数。
  
  git commit命令执行成功后会告诉你，1 file changed：1个文件被改动（我们新添加的readme.txt文件）；2 insertions：插入了两行内容（readme.txt有两行内容）。
  
  为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：
  $ git add file1.txt
  $ git add file2.txt file3.txt
  $ git commit -m "add 3 files."
  
  我们已经成功地添加并提交了一个readme.txt文件，现在，是时候继续工作了，于是，我们继续修改readme.txt文件，改成如下内容：
  Git is a distributed version control system.
  Git is free software.
  现在，运行git status命令看看结果：
  $ git status
  On branch master
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  	modified:   readme.txt
  no changes added to commit (use "git add" and/or "git commit -a")
  
  git status命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，readme.txt被修改过了，但还没有准备提交的修改。
  
  虽然Git告诉我们readme.txt被修改了，但如果能看看具体修改了什么内容，自然是很好的。比如你休假两周从国外回来，第一天上班时，已经记不清上次怎么修改的readme.txt，所以，需要用git diff这个命令看看：
  $ git diff readme.txt 
  diff --git a/readme.txt b/readme.txt
  index 46d49bf..9247db6 100644
  --- a/readme.txt
  +++ b/readme.txt
  @@ -1,2 +1,2 @@
  -Git is a version control system.
  +Git is a distributed version control system.
   Git is free software.
  git diff顾名思义就是查看difference，显示的格式正是Unix通用的diff格式，可以从上面的命令输出看到，我们在第一行添加了一个distributed单词。
  
  
  知道了对readme.txt作了什么修改后，再把它提交到仓库就放心多了，提交修改和提交新文件是一样的两步，第一步是git add：
  $ git add readme.txt
  
  
  同样没有任何输出。在执行第二步git commit之前，我们再运行git status看看当前仓库的状态：
  $ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  	modified:   readme.txt
  
  git status告诉我们，将要被提交的修改包括readme.txt，下一步，就可以放心地提交了：
  $ git commit -m "add distributed"
  [master e475afc] add distributed
   1 file changed, 1 insertion(+), 1 deletion(-)
  
  提交后，我们再用git status命令看看仓库的当前状态：
  $ git status
  On branch master
  nothing to commit, working tree clean
  Git告诉我们当前没有需要提交的修改，而且，工作目录是干净（working tree clean）的。
  
- 版本回退

  Git中每当文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在Git中被称为commit。一旦你把文件改乱了，或者误删了文件，还可以从最近的一个commit恢复，然后继续工作，而不是把几个月的工作成果全部丢失。
  
  现在，我们回顾一下readme.txt文件一共有几个版本被提交到Git仓库里了：
  
  版本1：wrote a readme file
  Git is a version control system.
  Git is free software.
  
  版本2：add distributed
  Git is a distributed version control system.
  Git is free software.
  
  版本3：append GPL
  Git is a distributed version control system.
  Git is free software distributed under the GPL.
  
  当然了，在实际工作中，怎么可能记得一个几千行的文件每次都改了什么内容，在Git中，用git log命令查看：
  $ git log
  commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master)
  Author: Michael Liao <askxuefeng@gmail.com>
  Date:   Fri May 18 21:06:15 2018 +0800
      append GPL
  commit e475afc93c209a690c39c13a46716e8fa000c366
  Author: Michael Liao <askxuefeng@gmail.com>
  Date:   Fri May 18 21:03:36 2018 +0800
      add distributed
  commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
  Author: Michael Liao <askxuefeng@gmail.com>
  Date:   Fri May 18 20:59:18 2018 +0800
      wrote a readme file
  
  git log命令显示从最近到最远的提交日志，我们可以看到3次提交，最近的一次是append GPL，上一次是add distributed，最早的一次是wrote a readme file。
  
  如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数：
  $ git log --pretty=oneline
  1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master) append GPL
  e475afc93c209a690c39c13a46716e8fa000c366 add distributed
  eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0 wrote a readme file
  
  需要友情提示的是，你看到的一大串类似1094adb...的是commit id（版本号），和SVN不一样，Git的commit id不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit id和我的肯定不一样，以你自己的为准。为什么commit id需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。
  
  每提交一个新版本，实际上Git就会把它们自动串成一条时间线。如果使用可视化工具查看Git历史，就可以更清楚地看到提交历史的时间线：
  
  ￼
  
  好了，现在我们启动时光穿梭机，准备把readme.txt回退到上一个版本，也就是add distributed的那个版本，怎么做呢？
  
  首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
  
  现在，我们要把当前版本append GPL回退到上一个版本add distributed，就可以使用git reset命令：
  $ git reset --hard HEAD^
  HEAD is now at e475afc add distributed
  
  看看readme.txt的内容是不是版本add distributed：
  $ cat readme.txt
  Git is a distributed version control system.
  Git is free software.
  
  果然被还原了。
  
  还可以继续回退到上一个版本wrote a readme file，不过且慢，让我们用git log再看看现在版本库的状态：
  $ git log
  commit e475afc93c209a690c39c13a46716e8fa000c366 (HEAD -> master)
  Author: Michael Liao <askxuefeng@gmail.com>
  Date:   Fri May 18 21:03:36 2018 +0800
  
      add distributed
  
  commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
  Author: Michael Liao <askxuefeng@gmail.com>
  Date:   Fri May 18 20:59:18 2018 +0800
  
      wrote a readme file
  
  最新的那个版本append GPL已经看不到了！好比你从21世纪坐时光穿梭机来到了19世纪，想再回去已经回不去了，肿么办？
  
  办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个append GPL的commit id是1094adb...，于是就可以指定回到未来的某个版本：
  $ git reset --hard 1094a
  HEAD is now at 83b0afe append GPL
  
  版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号，就无法确定是哪一个了。
  
  再小心翼翼地看看readme.txt的内容：
  $ cat readme.txt
  Git is a distributed version control system.
  Git is free software distributed under the GPL.
  
  Git的版本回退速度非常快，因为Git在内部有个指向当前版本的HEAD指针，当你回退版本的时候，Git仅仅是把HEAD从指向append GPL：
  ┌────┐
  │HEAD│
  └────┘
     │
     └──▶ ○ append GPL
          │
          ○ add distributed
          │
          ○ wrote a readme file
  
  改为指向add distributed：
  ┌────┐
  │HEAD│
  └────┘
     │
     │    ○ append GPL
     │    │
     └──▶ ○ add distributed
          │
          ○ wrote a readme file
  
  
  然后顺便把工作区的文件更新了。所以你让HEAD指向哪个版本号，你就把当前版本定位在哪。
  
  现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的commit id怎么办？
  
  在Git中，总是有后悔药可以吃的。当你用$ git reset --hard HEAD^回退到add distributed版本时，再想恢复到append GPL，就必须找到append GPL的commit id。Git提供了一个命令git reflog用来记录你的每一次命令：
  $ git reflog
  e475afc HEAD@{1}: reset: moving to HEAD^
  1094adb (HEAD -> master) HEAD@{2}: commit: append GPL
  e475afc HEAD@{3}: commit: add distributed
  eaadf4e HEAD@{4}: commit (initial): wrote a readme file
  
  终于舒了口气，从输出可知，append GPL的commit id是1094adb，现在，你又可以乘坐时光机回到未来了。
  
  小结
  HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
  穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
  要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
  
- 工作区和暂存区

  Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。
  
  先来看名词解释。
  工作区（Working Directory）
  就是你在电脑里能看到的目录，比如我的learngit文件夹就是一个工作区：
 
  版本库（Repository）
  工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
  
  Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

  
  前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：
  
  第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
  第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
  
  因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。
  你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。
  俗话说，实践出真知。现在，我们再练习一遍，先对readme.txt做个修改，比如加上一行内容：
  Git is a distributed version control system.
  Git is free software distributed under the GPL.
  Git has a mutable index called stage.
  
  然后，在工作区新增一个LICENSE文本文件（内容随便写）。
  先用git status查看一下状态：
  $ git status
  On branch master
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  	modified:   readme.txt
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
  	LICENSE
  no changes added to commit (use "git add" and/or "git commit -a")
  
  Git非常清楚地告诉我们，readme.txt被修改了，而LICENSE还从来没有被添加过，所以它的状态是Untracked。
  
  现在，使用两次命令git add，把readme.txt和LICENSE都添加后，用git status再查看一下：
  $ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
  	new file:   LICENSE
  	modified:   readme.txt
  
  现在，暂存区的状态就变成这样了：
  
  所以，git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。
  $ git commit -m "understand how stage works"
  [master e43a48b] understand how stage works
   2 files changed, 2 insertions(+)
   create mode 100644 LICENSE
  
  一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：
  $ git status
  On branch master
  nothing to commit, working tree clean
  
  现在版本库变成了这样，暂存区就没有任何内容了。￼
  
  
- 管理修改

  下面，我们要讨论的就是，为什么Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件。
  
  你会问，什么是修改？比如你新增了一行，这就是一个修改，删除了一行，也是一个修改，更改了某些字符，也是一个修改，删了一些又加了一些，也是一个修改，甚至创建一个新文件，也算一个修改。
  
  为什么说Git管理的是修改，而不是文件呢？我们还是做实验。第一步，对readme.txt做一个修改，比如加一行内容：
  $ cat readme.txt
  Git is a distributed version control system.
  Git is free software distributed under the GPL.
  Git has a mutable index called stage.
  Git tracks changes.
  
  然后，添加：
  $ git add readme.txt
  $ git status
  # On branch master
  # Changes to be committed:
  #   (use "git reset HEAD <file>..." to unstage)
  #
  #       modified:   readme.txt
  #
  
  然后，再修改readme.txt：
  $ cat readme.txt 
  Git is a distributed version control system.
  Git is free software distributed under the GPL.
  Git has a mutable index called stage.
  Git tracks changes of files.
  
  提交：
  $ git commit -m "git tracks changes"
  [master 519219b] git tracks changes
   1 file changed, 1 insertion(+)
  提交后，再看看状态：
  $ git status
  On branch master
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  
  	modified:   readme.txt
  
  no changes added to commit (use "git add" and/or "git commit -a")
  
  咦，怎么第二次的修改没有被提交？
  
  别激动，我们回顾一下操作过程：
  第一次修改 -> git add -> 第二次修改 -> git commit
  你看，我们前面讲了，Git管理的是修改，当你用git add命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，git commit只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。
  提交后，用git diff HEAD -- readme.txt命令可以查看工作区和版本库里面最新版本的区别：
  $ git diff HEAD -- readme.txt 
  diff --git a/readme.txt b/readme.txt
  index 76d770f..a9c5755 100644
  --- a/readme.txt
  +++ b/readme.txt
  @@ -1,4 +1,4 @@
   Git is a distributed version control system.
   Git is free software distributed under the GPL.
   Git has a mutable index called stage.
  -Git tracks changes.
  +Git tracks changes of files.
  
  可见，第二次修改确实没有被提交。
  那怎么提交第二次修改呢？你可以继续git add再git commit，也可以别着急提交第一次修改，先git add第二次修改，再git commit，就相当于把两次修改合并后一块提交了：
  第一次修改 -> git add -> 第二次修改 -> git add -> git commit
  
  提示：
  每次修改，如果不用git add到暂存区，那就不会加入到commit中。
  
- 撤销修改

  自然，你是不会犯错的。不过现在是凌晨两点，你正在赶一份工作报告，你在readme.txt中添加了一行：
  $ cat readme.txt
  Git is a distributed version control system.
  Git is free software distributed under the GPL.
  Git has a mutable index called stage.
  Git tracks changes of files.
  My stupid boss still prefers SVN.
  删掉最后一行，手动把文件恢复到上一个版本的状态。如果用git status查看一下：
  $ git status
  On branch master
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  
  	modified:   readme.txt
  
  no changes added to commit (use "git add" and/or "git commit -a")
  你可以发现，Git会告诉你，git checkout -- file可以丢弃工作区的修改：
  $ git checkout -- readme.txt
  命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
  
  一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
  一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
  总之，就是让这个文件回到最近一次git commit或git add时的状态。
  现在，看看readme.txt的文件内容：
  $ cat readme.txt
  Git is a distributed version control system.
  Git is free software distributed under the GPL.
  Git has a mutable index called stage.
  Git tracks changes of files.
  文件内容果然复原了。
  git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到git checkout命令。
  
  
  现在假定git add到暂存区了：
  $ cat readme.txt
  Git is a distributed version control system.
  Git is free software distributed under the GPL.
  Git has a mutable index called stage.
  Git tracks changes of files.
  My stupid boss still prefers SVN.
  
  $ git add readme.txt
  
  庆幸的是，在commit之前，你发现了这个问题。用git status查看一下，修改只是添加到了暂存区，还没有提交：
  $ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
  	modified:   readme.txt
  
  Git同样告诉我们，用命令git reset HEAD <file>可以把暂存区的修改撤销掉（unstage），重新放回工作区：
  $ git reset HEAD readme.txt
  Unstaged changes after reset:
  M	readme.txt
  
  git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。
  再用git status查看一下，现在暂存区是干净的，工作区有修改：
  $ git status
  On branch master
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  
  	modified:   readme.txt
  还记得如何丢弃工作区的修改吗？
  $ git checkout -- readme.txt
  
  $ git status
  On branch master
  nothing to commit, working tree clean
  
  现在，假设你不但改错了东西，还从暂存区提交到了版本库，怎么办呢？还记得版本回退吗？可以回退到上一个版本。不过，这是有条件的，就是你还没有把自己的本地版本库推送到远程。
  
  小结
  场景1：当改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
  场景2：当不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。
  场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
  
- 删除文件

  在Git中，删除也是一个修改操作，我们实战一下，先添加一个新文件test.txt到Git并且提交：
  $ git add test.txt
  
  $ git commit -m "add test.txt"
  [master b84166e] add test.txt
   1 file changed, 1 insertion(+)
   create mode 100644 test.txt
  一般情况下，通常直接在文件管理器中把没用的文件删了，或者用rm命令删了：
  $ rm test.txt
  这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了，git status命令会立刻告诉你哪些文件被删除了：
  $ git status
  On branch master
  Changes not staged for commit:
    (use "git add/rm <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  
  	deleted:    test.txt
  
  no changes added to commit (use "git add" and/or "git commit -a")
  现在有两个选择，一是确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit：
  $ git rm test.txt
  rm 'test.txt'
  
  $ git commit -m "remove test.txt"
  [master d46f35e] remove test.txt
   1 file changed, 1 deletion(-)
   delete mode 100644 test.txt
  现在，文件就从版本库中被删除了。
   小提示：先手动删除文件，然后使用git rm <file>和git add<file>效果是一样的。
  
  另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：
  $ git checkout -- test.txt
  git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
  
   注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！
  小结
  命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，只能恢复文件到最新版本，成功后会丢失最近一次提交后你修改的内容。
  
### 远程库

- 添加远程库

  现在的情景是，你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作，真是一举多得。
  首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：
  
  ￼
  
  在Repository name填入learngit，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：
  
  ￼
  
  目前，在GitHub上的这个learngit仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。
  
  现在，我们根据GitHub的提示，在本地的learngit仓库下运行命令：
  
  $ git remote add origin git@github.com:michaelliao/learngit.git
  请千万注意，把上面的michaelliao替换成你自己的GitHub账户名，否则，你在本地关联的就是我的远程库，关联没有问题，但是你以后推送是推不上去的，因为你的SSH Key公钥不在我的账户列表中。
  
  添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。
  
  下一步，就可以把本地库的所有内容推送到远程库上：
  $ git push -u origin master
  Counting objects: 20, done.
  Delta compression using up to 4 threads.
  Compressing objects: 100% (15/15), done.
  Writing objects: 100% (20/20), 1.64 KiB | 560.00 KiB/s, done.
  Total 20 (delta 5), reused 0 (delta 0)
  remote: Resolving deltas: 100% (5/5), done.
  To github.com:michaelliao/learngit.git
   * [new branch]      master -> master
  Branch 'master' set up to track remote branch 'master' from 'origin'.
  
  把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
  
  由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
  
  推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样：
  
  ￼
  
  从现在起，只要本地作了提交，就可以通过命令：
  $ git push origin master
  
  把本地master分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！
  
  SSH警告
  当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：
  The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
  RSA key fingerprint is xx.xx.xx.xx.xx.
  Are you sure you want to continue connecting (yes/no)?
  这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。
  
  Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：
  Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
  这个警告只会出现一次，后面的操作就不会有任何警告了。
  
  如果你实在担心有人冒充GitHub服务器，输入yes前可以对照GitHub的RSA Key的指纹信息是否与SSH连接给出的一致。
  
  删除远程库
  如果添加的时候地址写错了，或者就是想删除远程库，可以用git remote rm <name>命令。使用前，建议先用git remote -v查看远程库信息：
  $ git remote -v
  origin  git@github.com:michaelliao/learn-git.git (fetch)
  origin  git@github.com:michaelliao/learn-git.git (push)
  
  然后，根据名字删除，比如删除origin：
  $ git remote rm origin
  
  此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。
  
- 从远程库克隆

  上次我们讲了先有本地库，后有远程库的时候，如何关联远程库。
  
  现在，假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。
  首先，登陆GitHub，创建一个新的仓库，名字叫gitskills：
  
  ￼
  
  我们勾选Initialize this repository with a README，这样GitHub会自动为我们创建一个README.md文件。创建完毕后，可以看到README.md文件：
  
  ￼
  
  现在，远程库已经准备好了，下一步是用命令git clone克隆一个本地库：
  $ git clone git@github.com:michaelliao/gitskills.git
  Cloning into 'gitskills'...
  remote: Counting objects: 3, done.
  remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
  Receiving objects: 100% (3/3), done.
  
  注意把Git库的地址换成你自己的，然后进入gitskills目录看看，已经有README.md文件了：
  $ cd gitskills
  $ ls
  README.md
  
  如果有多个人协作开发，那么每个人各自从远程克隆一份就可以了。
  
  你也许还注意到，GitHub给出的地址不止一个，还可以用https://github.com/michaelliao/gitskills.git这样的地址。实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议。
  
  使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。
  
### 分支管理

- 创建与合并分支

  在版本回退里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。
  
  一开始的时候，master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，以及当前分支的提交点：
                    HEAD
                      │
                      │
                      ▼
                   master
                      │
                      │
                      ▼
  ┌───┐    ┌───┐    ┌───┐
  │   │───▶│   │───▶│   │
  └───┘    └───┘    └───┘
  
  每次提交，master分支都会向前移动一步，这样，随着你不断提交，master分支的线也越来越长。
  
  当我们创建新的分支，例如dev时，Git新建了一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上：
                   master
                      │
                      │
                      ▼
  ┌───┐    ┌───┐    ┌───┐
  │   │───▶│   │───▶│   │
  └───┘    └───┘    └───┘
                      ▲
                      │
                      │
                     dev
                      ▲
                      │
                      │
                    HEAD
  
  你看，Git创建一个分支很快，因为除了增加一个dev指针，改改HEAD的指向，工作区的文件都没有任何变化！
  
  不过，从现在开始，对工作区的修改和提交就是针对dev分支了，比如新提交一次后，dev指针往前移动一步，而master指针不变：
  
                   master
                      │
                      │
                      ▼
  ┌───┐    ┌───┐    ┌───┐    ┌───┐
  │   │───▶│   │───▶│   │───▶│   │
  └───┘    └───┘    └───┘    └───┘
                               ▲
                               │
                               │
                              dev
                               ▲
                               │
                               │
                             HEAD
  
  假如我们在dev上的工作完成了，就可以把dev合并到master上。Git怎么合并呢？最简单的方法，就是直接把master指向dev的当前提交，就完成了合并：
  
                             HEAD
                               │
                               │
                               ▼
                            master
                               │
                               │
                               ▼
  ┌───┐    ┌───┐    ┌───┐    ┌───┐
  │   │───▶│   │───▶│   │───▶│   │
  └───┘    └───┘    └───┘    └───┘
                               ▲
                               │
                               │
                              dev
  所以Git合并分支也很快！就改改指针，工作区内容也不变！
  
  合并完分支后，甚至可以删除dev分支。删除dev分支就是把dev指针给删掉，删掉后，我们就剩下了一条master分支：
                             HEAD
                               │
                               │
                               ▼
                            master
                               │
                               │
                               ▼
  ┌───┐    ┌───┐    ┌───┐    ┌───┐
  │   │───▶│   │───▶│   │───▶│   │
  └───┘    └───┘    └───┘    └───┘
  
  下面开始实战。
  
  首先，我们创建dev分支，然后切换到dev分支：
  $ git checkout -b dev
  Switched to a new branch 'dev'
  git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
  $ git branch dev
  $ git checkout dev
  Switched to branch 'dev'
  
  然后，用git branch命令查看当前分支：
  $ git branch
  * dev
    master
  
  git branch命令会列出所有分支，当前分支前面会标一个*号。
  
  然后，我们就可以在dev分支上正常提交，比如对readme.txt做个修改，加上一行：
  Creating a new branch is quick.
  
  然后提交：
  $ git add readme.txt 
  $ git commit -m "branch test"
  [dev b17d20e] branch test
   1 file changed, 1 insertion(+)
  
  现在，dev分支的工作完成，我们就可以切换回master分支：
  $ git checkout master
  Switched to branch 'master'
  
  切换回master分支后，再查看一个readme.txt文件，刚才添加的内容不见了！因为那个提交是在dev分支上，而master分支此刻的提交点并没有变：
  
  ￼
  
  现在，我们把dev分支的工作成果合并到master分支上：
  $ git merge dev
  Updating d46f35e..b17d20e
  Fast-forward
   readme.txt | 1 +
   1 file changed, 1 insertion(+)
  
  git merge命令用于合并指定分支到当前分支。合并后，再查看readme.txt的内容，就可以看到，和dev分支的最新提交是完全一样的。
  
  注意到上面的Fast-forward信息，Git告诉我们，这次合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快。
  
  当然，也不是每次合并都能Fast-forward，我们后面会讲其他方式的合并。
  
  合并完成后，就可以放心地删除dev分支了：
  $ git branch -d dev
  Deleted branch dev (was b17d20e).
  
  删除后，查看branch，就只剩下master分支了：
  $ git branch
  * master
  
  因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。
  switch
  
  我们注意到切换分支使用git checkout <branch>，而前面讲过的撤销修改则是git checkout -- <file>，同一个命令，有两种作用，确实有点令人迷惑。
  
  实际上，切换分支这个动作，用switch更科学。因此，最新版本的Git提供了新的git switch命令来切换分支：
  
  创建并切换到新的dev分支，可以使用：
  $ git switch -c dev
  
  直接切换到已有的master分支，可以使用：
  $ git switch master
  
  使用新的git switch命令，比git checkout要更容易理解。
  
  小结
  Git鼓励大量使用分支：
  查看分支：git branch
  创建分支：git branch <name>
  切换分支：git checkout <name>或者git switch <name>
  创建+切换分支：git checkout -b <name>或者git switch -c <name>
  合并某分支到当前分支：git merge <name>
  删除分支：git branch -d <name>
  
- 解决冲突

  合并分支往往也不是一帆风顺的。准备新的feature1分支，继续我们的新分支开发：
  $ git switch -c feature1
  Switched to a new branch 'feature1'
  
  修改readme.txt最后一行，改为：
  Creating a new branch is quick AND simple.
  
  在feature1分支上提交：
  $ git add readme.txt
  
  $ git commit -m "AND simple"
  [feature1 14096d0] AND simple
   1 file changed, 1 insertion(+), 1 deletion(-)
  
  切换到master分支：
  $ git switch master
  Switched to branch 'master'
  Your branch is ahead of 'origin/master' by 1 commit.
    (use "git push" to publish your local commits)
  
  Git还会自动提示我们当前master分支比远程的master分支要超前1个提交。
  在master分支上把readme.txt文件的最后一行改为：
  Creating a new branch is quick & simple.
  
  提交：
  $ git add readme.txt 
  $ git commit -m "& simple"
  [master 5dc6824] & simple
   1 file changed, 1 insertion(+), 1 deletion(-)
  
  现在，master分支和feature1分支各自都分别有新的提交，变成了这样：
                              HEAD
                                │
                                │
                                ▼
                             master
                                │
                                │
                                ▼
                              ┌───┐
                           ┌─▶│   │
  ┌───┐    ┌───┐    ┌───┐  │  └───┘
  │   │───▶│   │───▶│   │──┤
  └───┘    └───┘    └───┘  │  ┌───┐
                           └─▶│   │
                              └───┘
                                ▲
                                │
                                │
                            feature1
  
  这种情况下，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突，我们试试看：
  $ git merge feature1
  Auto-merging readme.txt
  CONFLICT (content): Merge conflict in readme.txt
  Automatic merge failed; fix conflicts and then commit the result.
  
  果然冲突了！Git告诉我们，readme.txt文件存在冲突，必须手动解决冲突后再提交。git status也可以告诉我们冲突的文件：
  $ git status
  On branch master
  Your branch is ahead of 'origin/master' by 2 commits.
    (use "git push" to publish your local commits)
  
  You have unmerged paths.
    (fix conflicts and run "git commit")
    (use "git merge --abort" to abort the merge)
  
  Unmerged paths:
    (use "git add <file>..." to mark resolution)
  
  	both modified:   readme.txt
  
  no changes added to commit (use "git add" and/or "git commit -a")
  
  我们可以直接查看readme.txt的内容：
  Git is a distributed version control system.
  Git is free software distributed under the GPL.
  Git has a mutable index called stage.
  Git tracks changes of files.
  <<<<<<< HEAD
  Creating a new branch is quick & simple.
  =======
  Creating a new branch is quick AND simple.
  >>>>>>> feature1
  
  Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，我们修改如下后保存：
  Creating a new branch is quick and simple.
  再提交：
  $ git add readme.txt 
  $ git commit -m "conflict fixed"
  [master cf810e4] conflict fixed
  现在，master分支和feature1分支变成了下图所示：
  
                                       HEAD
                                         │
                                         │
                                         ▼
                                      master
                                         │
                                         │
                                         ▼
                              ┌───┐    ┌───┐
                           ┌─▶│   │───▶│   │
  ┌───┐    ┌───┐    ┌───┐  │  └───┘    └───┘
  │   │───▶│   │───▶│   │──┤             ▲
  └───┘    └───┘    └───┘  │  ┌───┐      │
                           └─▶│   │──────┘
                              └───┘
                                ▲
                                │
                                │
                            feature1
  用带参数的git log也可以看到分支的合并情况：
  $ git log --graph --pretty=oneline --abbrev-commit
  *   cf810e4 (HEAD -> master) conflict fixed
  |\  
  | * 14096d0 (feature1) AND simple
  * | 5dc6824 & simple
  |/  
  * b17d20e branch test
  * d46f35e (origin/master) remove test.txt
  * b84166e add test.txt
  * 519219b git tracks changes
  * e43a48b understand how stage works
  * 1094adb append GPL
  * e475afc add distributed
  * eaadf4e wrote a readme file
  最后，删除feature1分支：
  $ git branch -d feature1
  Deleted branch feature1 (was 14096d0).
  工作完成。
  
  小结
  当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
  解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
  用git log --graph命令可以看到分支合并图。
  
- 分支管理策略

  通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
  
  如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
  
  下面我们实战一下--no-ff方式的git merge：
  
  首先，仍然创建并切换dev分支：
  $ git switch -c dev
  Switched to a new branch 'dev'
  修改readme.txt文件，并提交一个新的commit：
  $ git add readme.txt 
  $ git commit -m "add merge"
  [dev f52c633] add merge
   1 file changed, 1 insertion(+)
  现在，我们切换回master：
  $ git switch master
  Switched to branch 'master'
  准备合并dev分支，请注意--no-ff参数，表示禁用Fast forward：
  $ git merge --no-ff -m "merge with no-ff" dev
  Merge made by the 'recursive' strategy.
   readme.txt | 1 +
   1 file changed, 1 insertion(+)
  因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。
  
  合并后，我们用git log看看分支历史：
  $ git log --graph --pretty=oneline --abbrev-commit
  *   e1e9c68 (HEAD -> master) merge with no-ff
  |\  
  | * f52c633 (dev) add merge
  |/  
  *   cf810e4 conflict fixed
  ...
  
  可以看到，不使用Fast forward模式，merge后就像这样：
  
  ￼
  分支策略
  
  在实际开发中，我们应该按照几个基本原则进行分支管理：
  
  首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
  
  那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
  
  你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
  
  所以，团队合作的分支看起来就像这样：
  
  ￼
  小结
  Git分支十分强大，在团队开发中应该充分应用。
  合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
  
  
- Bug分支

  软件开发中，bug就像家常便饭一样。有了bug就需要修复，在Git中，由于分支是如此的强大，所以，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。
  
  当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复它，但是，等等，当前正在dev上进行的工作还没有提交：
  $ git status
  On branch dev
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
  	new file:   hello.py
  
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  
  	modified:   readme.txt
  
  并不是你不想提交，而是工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？
  
  幸好，Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：
  
  $ git stash
  Saved working directory and index state WIP on dev: f52c633 add merge
  
  
  现在，用git status查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug。
  
  
  首先确定要在哪个分支上修复bug，假定需要在master分支上修复，就从master创建临时分支：
  
  $ git checkout master
  Switched to branch 'master'
  Your branch is ahead of 'origin/master' by 6 commits.
    (use "git push" to publish your local commits)
  
  $ git checkout -b issue-101
  Switched to a new branch 'issue-101'
  
  
  现在修复bug，需要把“Git is free software ...”改为“Git is a free software ...”，然后提交：
  
  $ git add readme.txt 
  $ git commit -m "fix bug 101"
  [issue-101 4c805e2] fix bug 101
   1 file changed, 1 insertion(+), 1 deletion(-)
  
  
  修复完成后，切换到master分支，并完成合并，最后删除issue-101分支：
  
  $ git switch master
  Switched to branch 'master'
  Your branch is ahead of 'origin/master' by 6 commits.
    (use "git push" to publish your local commits)
  
  $ git merge --no-ff -m "merged bug fix 101" issue-101
  Merge made by the 'recursive' strategy.
   readme.txt | 2 +-
   1 file changed, 1 insertion(+), 1 deletion(-)
  
  
  太棒了，原计划两个小时的bug修复只花了5分钟！现在，是时候接着回到dev分支干活了！
  
  $ git switch dev
  Switched to branch 'dev'
  
  $ git status
  On branch dev
  nothing to commit, working tree clean
  
  
  工作区是干净的，刚才的工作现场存到哪去了？用git stash list命令看看：
  
  $ git stash list
  stash@{0}: WIP on dev: f52c633 add merge
  
  
  工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
  
  
  一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；
  
  
  另一种方式是用git stash pop，恢复的同时把stash内容也删了：
  
  $ git stash pop
  On branch dev
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
  	new file:   hello.py
  
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
  
  	modified:   readme.txt
  
  Dropped refs/stash@{0} (5d677e2ee266f39ea296182fb2354265b91b3b2a)
  
  
  再用git stash list查看，就看不到任何stash内容了：
  
  $ git stash list
  
  
  你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令：
  
  $ git stash apply stash@{0}
  
  
  在master分支上修复了bug后，我们要想一想，dev分支是早期从master分支分出来的，所以，这个bug其实在当前dev分支上也存在。
  
  
  那怎么在dev分支上修复同样的bug？重复操作一次，提交不就行了？
  
  
  有木有更简单的方法？
  
  
  有！
  
  
  同样的bug，要在dev上修复，我们只需要把4c805e2 fix bug 101这个提交所做的修改“复制”到dev分支。注意：我们只想复制4c805e2 fix bug 101这个提交所做的修改，并不是把整个master分支merge过来。
  
  
  为了方便操作，Git专门提供了一个cherry-pick命令，让我们能复制一个特定的提交到当前分支：
  
  $ git branch
  * dev
    master
  $ git cherry-pick 4c805e2
  [master 1d4b803] fix bug 101
   1 file changed, 1 insertion(+), 1 deletion(-)
  
  
  Git自动给dev分支做了一次提交，注意这次提交的commit是1d4b803，它并不同于master的4c805e2，因为这两个commit只是改动相同，但确实是两个不同的commit。用git cherry-pick，我们就不需要在dev分支上手动再把修bug的过程重复一遍。
  
  
  有些聪明的童鞋会想了，既然可以在master分支上修复bug后，在dev分支上可以“重放”这个修复过程，那么直接在dev分支上修复bug，然后在master分支上“重放”行不行？当然可以，不过你仍然需要git stash命令保存现场，才能从dev分支切换到master分支。
  
  小结
  
  
  修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
  
  
  当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场；
  
  
  在master分支上修复的bug，想要合并到当前dev分支，可以用git cherry-pick <commit>命令，把bug提交的修改“复制”到当前分支，避免重复劳动。
  
  
- Feature分支

  软件开发中，总有无穷无尽的新的功能要不断添加进来。
  
  
  添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。
  
  
  现在，你终于接到了一个新任务：开发代号为Vulcan的新功能，该功能计划用于下一代星际飞船。
  
  
  于是准备开发：
  
  $ git switch -c feature-vulcan
  Switched to a new branch 'feature-vulcan'
  
  
  5分钟后，开发完毕：
  
  $ git add vulcan.py
  
  $ git status
  On branch feature-vulcan
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
  	new file:   vulcan.py
  
  $ git commit -m "add feature vulcan"
  [feature-vulcan 287773e] add feature vulcan
   1 file changed, 2 insertions(+)
   create mode 100644 vulcan.py
  
  
  切回dev，准备合并：
  
  $ git switch dev
  
  
  一切顺利的话，feature分支和bug分支是类似的，合并，然后删除。
  
  
  但是！
  
  
  就在此时，接到上级命令，因经费不足，新功能必须取消！
  
  
  虽然白干了，但是这个包含机密资料的分支还是必须就地销毁：
  
  $ git branch -d feature-vulcan
  error: The branch 'feature-vulcan' is not fully merged.
  If you are sure you want to delete it, run 'git branch -D feature-vulcan'.
  
  
  销毁失败。Git友情提醒，feature-vulcan分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用大写的-D参数。。
  
  
  现在我们强行删除：
  
  $ git branch -D feature-vulcan
  Deleted branch feature-vulcan (was 287773e).
  
  
  终于删除成功！
  
  小结
  
  
  开发一个新feature，最好新建一个分支；
  
  
  如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。
  
  
- 多人协作

  当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。
  
  
  要查看远程库的信息，用git remote：
  
  $ git remote
  origin
  
  
  或者，用git remote -v显示更详细的信息：
  
  $ git remote -v
  origin  git@github.com:michaelliao/learngit.git (fetch)
  origin  git@github.com:michaelliao/learngit.git (push)
  
  
  上面显示了可以抓取和推送的origin的地址。如果没有推送权限，就看不到push的地址。
  
  推送分支
  
  
  推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：
  
  $ git push origin master
  
  
  如果要推送其他分支，比如dev，就改成：
  
  $ git push origin dev
  
  
  但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？
  
  master分支是主分支，因此要时刻与远程同步；
  
  dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
  
  bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
  
  feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
  
  
  总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定！
  
  抓取分支
  
  
  多人协作时，大家都会往master和dev分支上推送各自的修改。
  
  
  现在，模拟一个你的小伙伴，可以在另一台电脑（注意要把SSH Key添加到GitHub）或者同一台电脑的另一个目录下克隆：
  
  $ git clone git@github.com:michaelliao/learngit.git
  Cloning into 'learngit'...
  remote: Counting objects: 40, done.
  remote: Compressing objects: 100% (21/21), done.
  remote: Total 40 (delta 14), reused 40 (delta 14), pack-reused 0
  Receiving objects: 100% (40/40), done.
  Resolving deltas: 100% (14/14), done.
  
  
  当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的master分支。不信可以用git branch命令看看：
  
  $ git branch
  * master
  
  
  现在，你的小伙伴要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是他用这个命令创建本地dev分支：
  
  $ git checkout -b dev origin/dev
  
  
  现在，他就可以在dev上继续修改，然后，时不时地把dev分支push到远程：
  
  $ git add env.txt
  
  $ git commit -m "add env"
  [dev 7a5e5dd] add env
   1 file changed, 1 insertion(+)
   create mode 100644 env.txt
  
  $ git push origin dev
  Counting objects: 3, done.
  Delta compression using up to 4 threads.
  Compressing objects: 100% (2/2), done.
  Writing objects: 100% (3/3), 308 bytes | 308.00 KiB/s, done.
  Total 3 (delta 0), reused 0 (delta 0)
  To github.com:michaelliao/learngit.git
     f52c633..7a5e5dd  dev -> dev
  
  
  你的小伙伴已经向origin/dev分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送：
  
  $ cat env.txt
  env
  
  $ git add env.txt
  
  $ git commit -m "add new env"
  [dev 7bd91f1] add new env
   1 file changed, 1 insertion(+)
   create mode 100644 env.txt
  
  $ git push origin dev
  To github.com:michaelliao/learngit.git
   ! [rejected]        dev -> dev (non-fast-forward)
  error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
  hint: Updates were rejected because the tip of your current branch is behind
  hint: its remote counterpart. Integrate the remote changes (e.g.
  hint: 'git pull ...') before pushing again.
  hint: See the 'Note about fast-forwards' in 'git push --help' for details.
  
  
  推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送：
  
  $ git pull
  There is no tracking information for the current branch.
  Please specify which branch you want to merge with.
  See git-pull(1) for details.
  
      git pull <remote> <branch>
  
  If you wish to set tracking information for this branch you can do so with:
  
      git branch --set-upstream-to=origin/<branch> dev
  
  
  git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：
  
  $ git branch --set-upstream-to=origin/dev dev
  Branch 'dev' set up to track remote branch 'dev' from 'origin'.
  
  
  再pull：
  
  $ git pull
  Auto-merging env.txt
  CONFLICT (add/add): Merge conflict in env.txt
  Automatic merge failed; fix conflicts and then commit the result.
  
  
  这回git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push：
  
  $ git commit -m "fix env conflict"
  [dev 57c53ab] fix env conflict
  
  $ git push origin dev
  Counting objects: 6, done.
  Delta compression using up to 4 threads.
  Compressing objects: 100% (4/4), done.
  Writing objects: 100% (6/6), 621 bytes | 621.00 KiB/s, done.
  Total 6 (delta 0), reused 0 (delta 0)
  To github.com:michaelliao/learngit.git
     7a5e5dd..57c53ab  dev -> dev
  
  
  因此，多人协作的工作模式通常是这样：
  
  首先，可以试图用git push origin <branch-name>推送自己的修改；
  
  如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
  
  如果合并有冲突，则解决冲突，并在本地提交；
  
  没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
  
  
  如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
  
  
  这就是多人协作的工作模式，一旦熟悉了，就非常简单。
  
  小结
  
  查看远程库信息，使用git remote -v；
  
  本地新建的分支如果不推送到远程，对其他人就是不可见的；
  
  从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
  
  在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
  
  建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
  
  从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。
  
  
- Rebase

  在上一节我们看到了，多人在同一个分支上协作时，很容易出现冲突。即使没有冲突，后push的童鞋不得不先pull，在本地合并，然后才能push成功。
  
  
  每次合并再push后，分支变成了这样：
  
  $ git log --graph --pretty=oneline --abbrev-commit
  * d1be385 (HEAD -> master, origin/master) init hello
  *   e5e69f1 Merge branch 'dev'
  |\  
  | *   57c53ab (origin/dev, dev) fix env conflict
  | |\  
  | | * 7a5e5dd add env
  | * | 7bd91f1 add new env
  | |/  
  * |   12a631b merged bug fix 101
  |\ \  
  | * | 4c805e2 fix bug 101
  |/ /  
  * |   e1e9c68 merge with no-ff
  |\ \  
  | |/  
  | * f52c633 add merge
  |/  
  *   cf810e4 conflict fixed
  
  
  总之看上去很乱，有强迫症的童鞋会问：为什么Git的提交历史不能是一条干净的直线？
  
  
  其实是可以做到的！
  
  
  Git有一种称为rebase的操作，有人把它翻译成“变基”。
  
  ￼
  
  先不要随意展开想象。我们还是从实际问题出发，看看怎么把分叉的提交变成直线。
  
  
  在和远程分支同步后，我们对hello.py这个文件做了两次提交。用git log命令看看：
  
  $ git log --graph --pretty=oneline --abbrev-commit
  * 582d922 (HEAD -> master) add author
  * 8875536 add comment
  * d1be385 (origin/master) init hello
  *   e5e69f1 Merge branch 'dev'
  |\  
  | *   57c53ab (origin/dev, dev) fix env conflict
  | |\  
  | | * 7a5e5dd add env
  | * | 7bd91f1 add new env
  ...
  
  
  注意到Git用(HEAD -> master)和(origin/master)标识出当前分支的HEAD和远程origin的位置分别是582d922 add author和d1be385 init hello，本地分支比远程分支快两个提交。
  
  
  现在我们尝试推送本地分支：
  
  $ git push origin master
  To github.com:michaelliao/learngit.git
   ! [rejected]        master -> master (fetch first)
  error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
  hint: Updates were rejected because the remote contains work that you do
  hint: not have locally. This is usually caused by another repository pushing
  hint: to the same ref. You may want to first integrate the remote changes
  hint: (e.g., 'git pull ...') before pushing again.
  hint: See the 'Note about fast-forwards' in 'git push --help' for details.
  
  
  很不幸，失败了，这说明有人先于我们推送了远程分支。按照经验，先pull一下：
  
  $ git pull
  remote: Counting objects: 3, done.
  remote: Compressing objects: 100% (1/1), done.
  remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
  Unpacking objects: 100% (3/3), done.
  From github.com:michaelliao/learngit
     d1be385..f005ed4  master     -> origin/master
   * [new tag]         v1.0       -> v1.0
  Auto-merging hello.py
  Merge made by the 'recursive' strategy.
   hello.py | 1 +
   1 file changed, 1 insertion(+)
  
  
  再用git status看看状态：
  
  $ git status
  On branch master
  Your branch is ahead of 'origin/master' by 3 commits.
    (use "git push" to publish your local commits)
  
  nothing to commit, working tree clean
  
  
  加上刚才合并的提交，现在我们本地分支比远程分支超前3个提交。
  
  
  用git log看看：
  
  $ git log --graph --pretty=oneline --abbrev-commit
  *   e0ea545 (HEAD -> master) Merge branch 'master' of github.com:michaelliao/learngit
  |\  
  | * f005ed4 (origin/master) set exit=1
  * | 582d922 add author
  * | 8875536 add comment
  |/  
  * d1be385 init hello
  ...
  
  
  对强迫症童鞋来说，现在事情有点不对头，提交历史分叉了。如果现在把本地分支push到远程，有没有问题？
  
  
  有！
  
  
  什么问题？
  
  
  不好看！
  
  
  有没有解决方法？
  
  
  有！
  
  
  这个时候，rebase就派上了用场。我们输入命令git rebase试试：
  
  $ git rebase
  First, rewinding head to replay your work on top of it...
  Applying: add comment
  Using index info to reconstruct a base tree...
  M	hello.py
  Falling back to patching base and 3-way merge...
  Auto-merging hello.py
  Applying: add author
  Using index info to reconstruct a base tree...
  M	hello.py
  Falling back to patching base and 3-way merge...
  Auto-merging hello.py
  
  
  输出了一大堆操作，到底是啥效果？再用git log看看：
  
  $ git log --graph --pretty=oneline --abbrev-commit
  * 7e61ed4 (HEAD -> master) add author
  * 3611cfe add comment
  * f005ed4 (origin/master) set exit=1
  * d1be385 init hello
  ...
  
  
  原本分叉的提交现在变成一条直线了！这种神奇的操作是怎么实现的？其实原理非常简单。我们注意观察，发现Git把我们本地的提交“挪动”了位置，放到了f005ed4 (origin/master) set exit=1之后，这样，整个提交历史就成了一条直线。rebase操作前后，最终的提交内容是一致的，但是，我们本地的commit修改内容已经变化了，它们的修改不再基于d1be385 init hello，而是基于f005ed4 (origin/master) set exit=1，但最后的提交7e61ed4内容是一致的。
  
  
  这就是rebase操作的特点：把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。
  
  
  最后，通过push操作把本地分支推送到远程：
  
  Mac:~/learngit michael$ git push origin master
  Counting objects: 6, done.
  Delta compression using up to 4 threads.
  Compressing objects: 100% (5/5), done.
  Writing objects: 100% (6/6), 576 bytes | 576.00 KiB/s, done.
  Total 6 (delta 2), reused 0 (delta 0)
  remote: Resolving deltas: 100% (2/2), completed with 1 local object.
  To github.com:michaelliao/learngit.git
     f005ed4..7e61ed4  master -> master
  
  
  再用git log看看效果：
  
  $ git log --graph --pretty=oneline --abbrev-commit
  * 7e61ed4 (HEAD -> master, origin/master) add author
  * 3611cfe add comment
  * f005ed4 set exit=1
  * d1be385 init hello
  ...
  
  
  远程分支的提交历史也是一条直线。
  
  小结
  
  rebase操作可以把本地未push的分叉提交历史整理成直线；
  
  rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。
  
  
### 标签管理

- 创建标签

  在Git中打标签非常简单，首先，切换到需要打标签的分支上：
  
  $ git branch
  * dev
    master
  $ git checkout master
  Switched to branch 'master'
  
  
  然后，敲命令git tag <name>就可以打一个新标签：
  
  $ git tag v1.0
  
  
  可以用命令git tag查看所有标签：
  
  $ git tag
  v1.0
  
  
  默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？
  
  
  方法是找到历史提交的commit id，然后打上就可以了：
  
  $ git log --pretty=oneline --abbrev-commit
  12a631b (HEAD -> master, tag: v1.0, origin/master) merged bug fix 101
  4c805e2 fix bug 101
  e1e9c68 merge with no-ff
  f52c633 add merge
  cf810e4 conflict fixed
  5dc6824 & simple
  14096d0 AND simple
  b17d20e branch test
  d46f35e remove test.txt
  b84166e add test.txt
  519219b git tracks changes
  e43a48b understand how stage works
  1094adb append GPL
  e475afc add distributed
  eaadf4e wrote a readme file
  
  
  比方说要对add merge这次提交打标签，它对应的commit id是f52c633，敲入命令：
  
  $ git tag v0.9 f52c633
  
  
  再用命令git tag查看标签：
  
  $ git tag
  v0.9
  v1.0
  
  
  注意，标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname>查看标签信息：
  
  $ git show v0.9
  commit f52c63349bc3c1593499807e5c8e972b82c8f286 (tag: v0.9)
  Author: Michael Liao <askxuefeng@gmail.com>
  Date:   Fri May 18 21:56:54 2018 +0800
  
      add merge
  
  diff --git a/readme.txt b/readme.txt
  ...
  
  
  可以看到，v0.9确实打在add merge这次提交上。
  
  
  还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：
  
  $ git tag -a v0.1 -m "version 0.1 released" 1094adb
  
  
  用命令git show <tagname>可以看到说明文字：
  
  $ git show v0.1
  tag v0.1
  Tagger: Michael Liao <askxuefeng@gmail.com>
  Date:   Fri May 18 22:48:43 2018 +0800
  
  version 0.1 released
  
  commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (tag: v0.1)
  Author: Michael Liao <askxuefeng@gmail.com>
  Date:   Fri May 18 21:06:15 2018 +0800
  
      append GPL
  
  diff --git a/readme.txt b/readme.txt
  ...
  
   注意：标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。
  小结
  
  命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
  
  命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；
  
  命令git tag可以查看所有标签。
  
  
- 操作标签

  如果标签打错了，也可以删除：
  
  $ git tag -d v0.1
  Deleted tag 'v0.1' (was f15b0dd)
  
  
  因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。
  
  
  如果要推送某个标签到远程，使用命令git push origin <tagname>：
  
  $ git push origin v1.0
  Total 0 (delta 0), reused 0 (delta 0)
  To github.com:michaelliao/learngit.git
   * [new tag]         v1.0 -> v1.0
  
  
  或者，一次性推送全部尚未推送到远程的本地标签：
  
  $ git push origin --tags
  Total 0 (delta 0), reused 0 (delta 0)
  To github.com:michaelliao/learngit.git
   * [new tag]         v0.9 -> v0.9
  
  
  如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
  
  $ git tag -d v0.9
  Deleted tag 'v0.9' (was f52c633)
  
  
  然后，从远程删除。删除命令也是push，但是格式如下：
  
  $ git push origin :refs/tags/v0.9
  To github.com:michaelliao/learngit.git
   - [deleted]         v0.9
  
  
  要看看是否真的从远程库删除了标签，可以登陆GitHub查看。
  
  小结
  
  命令git push origin <tagname>可以推送一个本地标签；
  
  命令git push origin --tags可以推送全部未推送过的本地标签；
  
  命令git tag -d <tagname>可以删除一个本地标签；
  
  命令git push origin :refs/tags/<tagname>可以删除一个远程标签。
  
  
### 自定义Git

- 忽略特殊文件

  有些时候，你必须把某些文件放到Git工作目录中，但又不能提交它们，比如保存了数据库密码的配置文件啦，等等，每次git status都会显示Untracked files ...，有强迫症的童鞋心里肯定不爽。
  
  
  好在Git考虑到了大家的感受，这个问题解决起来也很简单，在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。
  
  
  不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：https://github.com/github/gitignore
  
  
  忽略文件的原则是：
  
  忽略操作系统自动生成的文件，比如缩略图等；
  忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
  忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。
  
  举个例子：
  
  
  假设你在Windows下进行Python开发，Windows会自动在有图片的目录下生成隐藏的缩略图文件，如果有自定义目录，目录下就会有Desktop.ini文件，因此你需要忽略Windows自动生成的垃圾文件：
  
  # Windows:
  Thumbs.db
  ehthumbs.db
  Desktop.ini
  
  
  然后，继续忽略Python编译产生的.pyc、.pyo、dist等文件或目录：
  
  # Python:
  *.py[cod]
  *.so
  *.egg
  *.egg-info
  dist
  build
  
  
  加上你自己定义的文件，最终得到一个完整的.gitignore文件，内容如下：
  
  # Windows:
  Thumbs.db
  ehthumbs.db
  Desktop.ini
  
  # Python:
  *.py[cod]
  *.so
  *.egg
  *.egg-info
  dist
  build
  
  # My configurations:
  db.ini
  deploy_key_rsa
  
  
  最后一步就是把.gitignore也提交到Git，就完成了！当然检验.gitignore的标准是git status命令是不是说working directory clean。
  
  
  使用Windows的童鞋注意了，如果你在资源管理器里新建一个.gitignore文件，它会非常弱智地提示你必须输入文件名，但是在文本编辑器里“保存”或者“另存为”就可以把文件保存为.gitignore了。
  
  
  有些时候，你想添加一个文件到Git，但发现添加不了，原因是这个文件被.gitignore忽略了：
  
  $ git add App.class
  The following paths are ignored by one of your .gitignore files:
  App.class
  Use -f if you really want to add them.
  
  
  如果你确实想添加该文件，可以用-f强制添加到Git：
  
  $ git add -f App.class
  
  
  或者你发现，可能是.gitignore写得有问题，需要找出来到底哪个规则写错了，可以用git check-ignore命令检查：
  
  $ git check-ignore -v App.class
  .gitignore:3:*.class	App.class
  
  
  Git会告诉我们，.gitignore的第3行规则忽略了该文件，于是我们就可以知道应该修订哪个规则。
  
  
  还有些时候，当我们编写了规则排除了部分文件时：
  
  # 排除所有.开头的隐藏文件:
  .*
  # 排除所有.class文件:
  *.class
  
  
  但是我们发现.*这个规则把.gitignore也排除了，并且App.class需要被添加到版本库，但是被*.class规则排除了。
  
  
  虽然可以用git add -f强制添加进去，但有强迫症的童鞋还是希望不要破坏.gitignore规则，这个时候，可以添加两条例外规则：
  
  # 排除所有.开头的隐藏文件:
  .*
  # 排除所有.class文件:
  *.class
  
  # 不排除.gitignore和App.class:
  !.gitignore
  !App.class
  
  
  把指定文件排除在.gitignore规则外的写法就是!+文件名，所以，只需把例外文件添加进去即可。
  
  
  可以通过https://gitignore.itranswarp.com在线生成.gitignore文件。
  
  小结
  
  忽略某些文件时，需要编写.gitignore；
  
  .gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！
  
  
- 配置别名

  有没有经常敲错命令？比如git status？status这个单词真心不好记。
  
  
  如果敲git st就表示git status那就简单多了，当然这种偷懒的办法我们是极力赞成的。
  
  
  我们只需要敲一行命令，告诉Git，以后st就表示status：
  
  $ git config --global alias.st status
  
  
  好了，现在敲git st看看效果。
  
  
  当然还有别的命令可以简写，很多人都用co表示checkout，ci表示commit，br表示branch：
  
  $ git config --global alias.co checkout
  $ git config --global alias.ci commit
  $ git config --global alias.br branch
  
  
  以后提交就可以简写成：
  
  $ git ci -m "bala bala bala..."
  
  
  --global参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。
  
  
  在撤销修改一节中，我们知道，命令git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区。既然是一个unstage操作，就可以配置一个unstage别名：
  
  $ git config --global alias.unstage 'reset HEAD'
  
  
  当你敲入命令：
  
  $ git unstage test.py
  
  
  实际上Git执行的是：
  
  $ git reset HEAD test.py
  
  
  配置一个git last，让其显示最后一次提交信息：
  
  $ git config --global alias.last 'log -1'
  
  
  这样，用git last就能显示最近一次的提交：
  
  $ git last
  commit adca45d317e6d8a4b23f9811c3d7b7f0f180bfe2
  Merge: bd6ae48 291bea8
  Author: Michael Liao <askxuefeng@gmail.com>
  Date:   Thu Aug 22 22:49:22 2013 +0800
  
      merge & fix hello.py
  
  
  甚至还有人丧心病狂地把lg配置成了：
  
  git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
  
  
  来看看git lg的效果：
  
  ￼
  
  为什么不早点告诉我？别激动，咱不是为了多记几个英文单词嘛！
  
  配置文件
  
  
  配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。
  
  
  配置文件放哪了？每个仓库的Git配置文件都放在.git/config文件中：
  
  $ cat .git/config 
  [core]
      repositoryformatversion = 0
      filemode = true
      bare = false
      logallrefupdates = true
      ignorecase = true
      precomposeunicode = true
  [remote "origin"]
      url = git@github.com:michaelliao/learngit.git
      fetch = +refs/heads/*:refs/remotes/origin/*
  [branch "master"]
      remote = origin
      merge = refs/heads/master
  [alias]
      last = log -1
  
  
  别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。
  
  
  而当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中：
  
  $ cat .gitconfig
  [alias]
      co = checkout
      ci = commit
      br = branch
      st = status
  [user]
      name = Your Name
      email = your@email.com
  
  
  配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。
  
  小结
  
  
  给Git配置好别名，就可以输入命令时偷个懒。我们鼓励偷懒。
  
  
- 搭建Git服务器

  在远程仓库一节中，我们讲了远程仓库实际上和本地仓库没啥不同，纯粹为了7x24小时开机并交换大家的修改。
  
  
  GitHub就是一个免费托管开源代码的远程仓库。但是对于某些视源代码如生命的商业公司来说，既不想公开源代码，又舍不得给GitHub交保护费，那就只能自己搭建一台Git服务器作为私有仓库使用。
  
  
  搭建Git服务器需要准备一台运行Linux的机器，强烈推荐用Ubuntu或Debian，这样，通过几条简单的apt命令就可以完成安装。
  
  
  假设你已经有sudo权限的用户账号，下面，正式开始安装。
  
  
  第一步，安装git：
  
  $ sudo apt-get install git
  
  
  第二步，创建一个git用户，用来运行git服务：
  
  $ sudo adduser git
  
  
  第三步，创建证书登录：
  
  
  收集所有需要登录的用户的公钥，就是他们自己的id_rsa.pub文件，把所有公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。
  
  
  第四步，初始化Git仓库：
  
  先选定一个目录作为Git仓库，假定是/srv/sample.git，在/srv目录下输入命令：
  
  $ sudo git init --bare sample.git
  
  
  Git就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以.git结尾。然后，把owner改为git：
  
  $ sudo chown -R git:git sample.git
  
  
  第五步，禁用shell登录：
  
  
  出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑/etc/passwd文件完成。找到类似下面的一行：
  
  git:x:1001:1001:,,,:/home/git:/bin/bash
  
  
  改为：
  
  git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
  
  
  这样，git用户可以正常通过ssh使用git，但无法登录shell，因为我们为git用户指定的git-shell每次一登录就自动退出。
  
  
  第六步，克隆远程仓库：
  
  
  现在，可以通过git clone命令克隆远程仓库了，在各自的电脑上运行：
  
  $ git clone git@server:/srv/sample.git
  Cloning into 'sample'...
  warning: You appear to have cloned an empty repository.
  
  
  剩下的推送就简单了。
  
  管理公钥
  
  
  如果团队很小，把每个人的公钥收集起来放到服务器的/home/git/.ssh/authorized_keys文件里就是可行的。如果团队有几百号人，就没法这么玩了，这时，可以用Gitosis来管理公钥。
  
  
  这里我们不介绍怎么玩Gitosis了，几百号人的团队基本都在500强了，相信找个高水平的Linux管理员问题不大。
  
  管理权限
  
  
  有很多不但视源代码如生命，而且视员工为窃贼的公司，会在版本控制系统里设置一套完善的权限控制，每个人是否有读写权限会精确到每个分支甚至每个目录下。因为Git是为Linux源代码托管而开发的，所以Git也继承了开源社区的精神，不支持权限控制。不过，因为Git支持钩子（hook），所以，可以在服务器端编写一系列脚本来控制提交等操作，达到权限控制的目的。Gitolite就是这个工具。
  
  
  这里我们也不介绍Gitolite了，不要把有限的生命浪费到权限斗争中。
  
  小结
  
  搭建Git服务器非常简单，通常10分钟即可完成；
  
  要方便管理公钥，用Gitosis；
  
  要像SVN那样变态地控制权限，用Gitolite。
  
  
### 使用SourceTree

当我们对Git的提交、分支已经非常熟悉，可以熟练使用命令操作Git后，再使用GUI工具，就可以更高效。

Git有很多图形界面工具，这里我们推荐SourceTree，它是由Atlassian开发的免费Git图形界面工具，可以操作任何Git库。
首先从官网下载SourceTree并安装，然后直接运行SourceTree。
第一次运行SourceTree时，SourceTree并不知道我们的Git库在哪。如果本地已经有了Git库，直接从资源管理器把文件夹拖拽到SourceTree上，就添加了一个本地Git库：
也可以选择“New”-“Clone from URL”直接从远程克隆到本地。

提交
我们双击learngit这个本地库，SourceTree会打开另一个窗口，展示这个Git库的当前所有分支以及文件状态。选择左侧面板的“WORKSPACE”-“File status”，右侧会列出当前已修改的文件（Unstaged files）：
选中某个文件，该文件就自动添加到“Staged files”，实际上是执行了git add README.md命令：
然后，我们在下方输入Commit描述，点击“Commit”，就完成了一个本地提交：
实际上是执行了git commit -m "update README.md"命令。
使用SourceTree进行提交就是这么简单，它的优势在于可以可视化地观察文件的修改，并以红色和绿色高亮显示。

分支
在左侧面板的“BRANCHES”下，列出了当前本地库的所有分支。当前分支会加粗并用○标记。要切换分支，我们只需要选择该分支，例如master，然后点击右键，在弹出菜单中选择“Checkout master”，实际上是执行命令git checkout master：
要合并分支，同样选择待合并分支，例如dev，然后点击右键，在弹出菜单中选择“Merge dev into master”，实际上是执行命令git merge dev：

推送
在SourceTree的工具栏上，分别有Pull和Push，分别对应命令git pull和git push，只需注意本地和远程分支的名称要对应起来，使用时十分简单。
注意到使用SourceTree时，我们只是省下了敲命令的麻烦，SourceTree本身还是通过Git命令来执行任何操作。如果操作失败，SourceTree会自动显示执行的Git命令以及错误信息，我们可以通过Git返回的错误信息知道出错的原因：

小结
使用SourceTree可以以图形界面操作Git，省去了敲命令的过程，对于常用的提交、分支、推送等操作来说非常方便。
SourceTree使用Git命令执行操作，出错时，仍然需要阅读Git命令返回的错误信息。


5.策划案
游戏名称：Unity单人坦克大战

概述：
Unity单人坦克大战是一款以动作和策略为核心的单人游戏。玩家将扮演一名坦克指挥官，在战斗场景中面对不同的敌人和挑战。玩家需要操控自己的坦克，破坏敌人并完成各种任务，通过挑战和升级来提升自己的技能和装备。

游戏目标：
- 摧毁敌人的坦克和设施
- 完成各种任务和关卡
- 收集资源和升级自己的坦克

游戏要素：
1. 坦克角色：玩家以坦克指挥官的身份，可以选择不同类型的坦克。每种坦克都有独特的属性和技能，如攻击力、防御力和移动速度等。
2. 关卡任务：游戏中包含多个关卡，每个关卡都有特定的任务和目标。任务可以包括摧毁敌人、保护盟友、收集特定物品等，玩家需要根据任务要求来完成关卡。
3. 敌人AI：游戏中的敌人坦克由AI控制，它们会根据玩家的位置和行动来进行攻击和防御。敌人AI的难度会随着玩家的进展逐渐增加，增加游戏的挑战性。
4. 资源收集：在游戏中，玩家可以收集资源，如金币、弹药等，用于升级坦克和购买新的装备和道具。
5. 升级系统：玩家可以使用收集到的资源来升级自己的坦克。升级可以提升坦克的属性和技能，使玩家更强大和适应不同的战斗情况。
6. 战斗场景：游戏中拥有多个战斗场景，如城市、沙漠和森林等。每个场景都有独特的地形和障碍物，玩家需要灵活运用地形进行战术和躲避敌人的攻击。
7. 视角切换: 玩家可以在游戏中选择使用胜利视角或者第一/第三人称视角进行游戏。不同的视角可以让玩家获得不同的游戏体验和操作感。
8. 血条和护甲: 玩家的坦克增加血条显示，同时引入护甲系统。血条显示玩家当前的血量状态，护甲可以吸收一定量的攻击伤害，提高坦克的续航能力。
9. 移动策略: 在坦克移动方面引入惯性和耗油等概念。坦克的移动具有一定的惯性效果，需要玩家灵活操作以适应移动状态的变化。同时，移动过程中耗油量增加，玩家需要合理规划油耗与行动范围。
10. 子弹效果升级: 玩家可以购买和升级不同类型的子弹来增强攻击力，改变射程和速度，提升装填速度等。不同的子弹效果可根据不同敌人的特点和场景来进行选择和应对。
11. 拾取物品: 在游戏中添加可拾取的物品，如补给包和特殊道具，玩家可以拾取它们来恢复血量、补充弹药或者获取特殊效果。拾取物品能够帮助玩家在战斗中更好地维持自身状态。
12. 成就系统: 添加成就系统来增加游戏的挑战性和长久性。玩家可以在游戏过程中完成特定的任务和目标，解锁丰厚的成就奖励以及额外的游戏挑战。

游戏流程：
1. 开始游戏：玩家选择角色和关卡，进入游戏界面。
2. 进行关卡任务：玩家操控自己的坦克，按照任务要求进行战斗和行动。
3. 战斗和升级：玩家需要摧毁敌人坦克和设施，收集资源并进行升级，提升自己的能力。
4. 完成关卡：玩家完成关卡任务后，根据表现给予评价和奖励，解锁新的关卡和装备。
5. 进行下一关卡：玩家可以选择继续挑战下一个关卡，或者回到主菜单进行其他操作。

扩展想法：
- Boss战：在特定的关卡中添加强大的BOSS敌人，玩家需要与其进行对战并击败。每个BOSS都有独特的技能和战斗方式，玩家需要掌握它们的弱点并采取正确的策略来击败它们。
- 故事模式：为游戏添加一个丰富的故事背景和剧情，通过解锁关卡和完成任务来逐步揭示故事情节。
- 排行榜和挑战模式：添加排行榜系统，玩家可以比较自己在不同关卡的成绩。同时，添加特殊的挑战关卡，玩家可以尝试挑战自己的极限和获取额外的奖励。
- 自定关卡编辑器：为玩家提供自定义关卡的功能，可以自己设计并分享关卡给其他玩家挑战。

合作方式：
为了更好地实现上述改进和新增内容，建议在策划和程序之间进行紧密合作。策划需提供详细的需求和设计思路，程序将根据这些需求进行技术上的实现。双方密切沟通和协作，保证游戏的可行性、难度适宜以及开发时间的控制。



6.思考题
Buff移除功能相关代码：
```csharp
public class Buff
{
    protected Player player;
    protected float duration;

    public Buff(Player player, float duration)
    {
        this.player = player;
        this.duration = duration;
    }

    public virtual void Apply()
    {
        // 应用Buff效果
    }

    public virtual void OnRemove()
    {
        // 移除Buff效果
    }
}

public class SpeedBuff : Buff
{
    private float speedIncrease;

    public SpeedBuff(Player player, float duration, float speedIncrease) : base(player, duration)
    {
        this.speedIncrease = speedIncrease;
    }

    public override void Apply()
    {
        // 增加玩家速度
        player.speed += speedIncrease;
    }

    public override void OnRemove()
    {
        // 移除玩家速度增益
        player.speed -= speedIncrease;
    }
}
```
HpBuff的相关代码：

```csharp
public class HpBuff : Buff
{
    private int hpIncrease;

    public HpBuff(Player player, float duration, int hpIncrease) : base(player, duration)
    {
        this.hpIncrease = hpIncrease;
    }

    public override void Apply()
    {
        // 增加玩家血量
        player.hp += hpIncrease;
    }

    public override void OnRemove()
    {
        // 移除玩家血量增益
        player.hp -= hpIncrease;
    }
}
```
扩展问题：如果想要能显示玩家此时身上拥有哪些Buff，可以在Player类中添加一个List来存储玩家当前的Buff。在Buff类中添加一个字符串属性来表示Buff的名字。当玩家获得一个新的Buff时，将其添加到Buff列表中。可以通过循环遍历Buff列表，并将Buff的名字显示在UI界面上从而实现显示玩家身上拥有的Buff的功能。