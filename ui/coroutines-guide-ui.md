<!--- INCLUDE .*/example-ui-([a-z]+)-([0-9]+)\.kt 
/*
 * Copyright 2016-2017 JetBrains s.r.o.
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 * http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

// This file was automatically generated from coroutines-guide-ui.md by Knit tool. Do not edit.
package guide.ui.$$1.example$$2

import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.channels.*
import kotlinx.coroutines.experimental.javafx.JavaFx as UI
import javafx.application.Application
import javafx.event.EventHandler
import javafx.geometry.*
import javafx.scene.*
import javafx.scene.input.MouseEvent
import javafx.scene.layout.StackPane
import javafx.scene.paint.Color
import javafx.scene.shape.Circle
import javafx.scene.text.Text
import javafx.stage.Stage

fun main(args: Array<String>) {
    Application.launch(ExampleApp::class.java, *args)
}

class ExampleApp : Application() {
    val hello = Text("Hello World!").apply {
        fill = Color.valueOf("#C0C0C0")
    }

    val fab = Circle(20.0, Color.valueOf("#FF4081"))

    val root = StackPane().apply {
        children += hello
        children += fab
        StackPane.setAlignment(hello, Pos.CENTER)
        StackPane.setAlignment(fab, Pos.BOTTOM_RIGHT)
        StackPane.setMargin(fab, Insets(15.0))
    }

    val scene = Scene(root, 240.0, 380.0).apply {
        fill = Color.valueOf("#303030")
    }

    override fun start(stage: Stage) {
        stage.title = "Example"
        stage.scene = scene
        stage.show()
        setup(hello, fab)
    }
}
-->
<!--- KNIT     kotlinx-coroutines-javafx/src/test/kotlin/guide/.*\.kt -->

# �R���[�`���ɂ��UI�v���O���~���O�K�C�h

���̃K�C�h�́A[kotlinx.coroutines�̃K�C�h](../coroutines-guide.md)�ŃJ�o�[����Ă����{�I�ȃR���[�`���̊T�O�ɐ��ʂ��Ă��邱�Ƃ�O��Ƃ��Ă���AUI�A�v���P�[�V�����ŃR���[�`�����g�p������@�̋�̗�������Ă��܂��B

���ׂĂ�UI�A�v���P�[�V�������C�u�����ɋ��ʂ���1�̂��Ƃ�����܂��B UI�̂��ׂĂ̏�Ԃ��S�������P��̃X���b�h������A���̓���̃X���b�h��UI�ɑ΂��邷�ׂĂ̍X�V���s���Ȃ���΂Ȃ�܂���B �R���[�`���Ɋւ��ẮA�R���[�`���̎��s������UI�X���b�h�ɍS������K�؂� _�R���[�`���f�B�X�p�b�`���[�R���e�L�X�g_ ���K�v�ł��邱�Ƃ��Ӗ����܂��B

��̓I�ɂ́A `kotlinx.coroutines` �͈قȂ�UI�A�v���P�[�V�������C�u�����ɃR���[�`���̃R���e�L�X�g��񋟂���3�̃��W���[���������Ă��܂��B
 
* [kotlinx-coroutines-android](kotlinx-coroutines-android) -- Android�A�v���P�[�V�����̂��߂� `UI` �R���e�L�X�g�B
* [kotlinx-coroutines-javafx](kotlinx-coroutines-javafx) -- JavaFX UI�A�v���P�[�V�����̂��߂� `JavaFx` �R���e�L�X�g�B
* [kotlinx-coroutines-swing](kotlinx-coroutines-swing) -- Swing UI �A�v���P�[�V�����̂��߂� `Swing` �R���e�L�X�g�B

���̃K�C�h�ł́A���ׂĂ�UI���C�u�����𓯎��Ɉ����܂��B�Ȃ��Ȃ�A�����̃��W���[���̂��ꂼ��́A���y�[�W�̒����̂���1�����̃I�u�W�F�N�g��`���琬���Ă��邩��ł��B �����ɂ͊܂܂�Ă��Ȃ��Ă��A�����̂ǂꂩ���Ƃ��Ďg���āA�D�݂�UI���C�u�����p�̑Ή�����R���e�L�X�g�I�u�W�F�N�g���������Ƃ��ł��܂��B

## �ڎ�

<!--- TOC -->

* [�Z�b�g�A�b�v](#�Z�b�g�A�b�v)
  * [JavaFx](#javafx)
  * [Android](#android)
* [��{�I��UI�R���[�`��](#��{�I��ui�R���[�`��)
  * [UI�R���[�`���̋N��](#ui�R���[�`���̋N��)
  * [UI�R���[�`���̃L�����Z��](#ui�R���[�`���̃L�����Z��)
* [UI�R���e�L�X�g���ł̃A�N�^�[�̎g�p](#ui�R���e�L�X�g���ł̃A�N�^�[�̎g�p)
  * [�R���[�`���̂��߂̊g��](#�R���[�`���̂��߂̊g��)
  * [�ő��1�̓����W���u](#�ő��1�̓����W���u)
  * [�C�x���g�̍���](#�C�x���g�̍���)
* [�u���b�L���O����](#�u���b�L���O����)
  * [UI�t���[�Y���](#ui�t���[�Y���)
  * [�u���b�L���O����](#�u���b�L���O����)
* [���x�ȃg�s�b�N](#���x�ȃg�s�b�N)
  * [���C�t�T�C�N���ƃR���[�`���̐e�q�K�w](#���C�t�T�C�N���ƃR���[�`���̐e�q�K�w)
  * [�f�B�X�p�b�`������UI�C�x���g�n���h���ŃR���[�`�����J�n����](#�f�B�X�p�b�`������ui�C�x���g�n���h���ŃR���[�`�����J�n����)

<!--- END_TOC -->

## �Z�b�g�A�b�v

���̃K�C�h�̎��s�\�ȗ�́AJavaFx�p�ɒ񋟂���Ă��܂��B ���_�́A�G�~�����[�^�Ȃǂ�K�v�Ƃ����ɂ��ׂẴT���v����C�ӂ�OS�Œ��ڋN���ł��A���S�Ɏ��Ȋ������Ă��邱�Ƃł��i�e���1�̃t�@�C���ɂ���܂��j�B
Android�ł������Č����邽�߂ɕK�v�ȕύX�_�i��������΁j�ɂ��ĕʓr����������܂��B

### JavaFx

JavaFx�̊�{�I�ȃA�v���P�[�V�����̗�́A�ŏ��ɕ����� "Hello World�I" ���܂� `hello` �Ƃ������O�̃e�L�X�g���x���ƁA�E���� `fab` �i�t���[�e�B���O�A�N�V�����{�^���j�Ƃ������O�̃s���N�̉~�����E�B���h�E�ō\������Ă��܂��B

![UI example for JavaFx](ui-example-javafx.png)

JavaFX�A�v���P�[�V������ `start` �֐��� `hello` �� `fab` �m�[�h�ւ̎Q�Ƃ�n�� `setup` �֐����Ăяo���܂��B
�����ɂ́A���̃K�C�h�̎c��̕����ł��܂��܂ȃR�[�h���L�q���Ă��܂��B

```kotlin
fun setup(hello: Text, fab: Circle) {
    // placeholder
}
```

> [����](kotlinx-coroutines-javafx/src/test/kotlin/guide/example-ui-basic-01.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

GitHub��[kotlinx.coroutines](https://github.com/Kotlin/kotlinx.coroutines)�v���W�F�N�g�����[�N�X�e�[�V�����ɃN���[�����AIDE�Ńv���W�F�N�g���J�����Ƃ��ł��܂��B ���̃K�C�h�̂��ׂĂ̗�́A[`ui/kotlinx-coroutines-javafx`](kotlinx-coroutines-javafx)���W���[���̃e�X�g�t�H���_�ɂ���܂��B
����ɂ��A�e�T���v�����ǂ̂悤�ɓ��삷�邩���m�F���A�ύX���Ď������邱�Ƃ��ł��܂��B

### Android

Android Studio��Kotlin�v���W�F�N�g���쐬����ɂ́A[Getting Started With Android and Kotlin](https://kotlinlang.org/docs/tutorials/kotlin-android.html)�̃K�C�h�ɏ]���Ă��������B �A�v���P�[�V������[Kotlin Android Extensions](https://kotlinlang.org/docs/tutorials/android-plugin.html)��ǉ����邱�Ƃ������߂��܂��B

Android Studio 2.3�ł́A���̂悤�ȃA�v���P�[�V�������\������܂��B

![UI example for Android](ui-example-android.png)

�A�v���P�[�V������ `context_main.xml` �Ɉړ����A������ "Hello World�I"���������e�L�X�g�r���[�� "hello" �Ƃ���ID�����蓖�Ă܂��B ����́A���Ȃ��̃A�v���P�[�V�����ŁAKotlin Android�g���@�\���� `hello` �Ƃ��ė��p�ł���悤�ɂ��邽�߂ł��B
�s���N�F�̃t���[�e�B���O�A�N�V�����{�^���́A�쐬���ꂽ�v���W�F�N�g�e���v���[�g���Ŋ��� `fab` �Ƃ������O���t���Ă��܂��B

�A�v���P�[�V������ `MainActivity.kt` �ł� `fab.setOnClickListener {...}` �u���b�N���폜���A����� `onCreate` �֐��̍Ō�̍s�Ƃ��� `setup(hello�Afab)` �Ăяo����ǉ����܂��B
�t�@�C���̍Ō�Ƀv���[�X�z���_�[�� `setup` �֐����쐬���܂��B
�����ɂ́A���̃K�C�h�̈ȍ~�̕����ł��܂��܂ȃR�[�h���L�q���Ă��܂��B

```kotlin
fun setup(hello: TextView, fab: FloatingActionButton) {
    // placeholder
}
```

<!--- CLEAR -->

`kotlinx-coroutines-android` ���W���[���ւ̈ˑ��֌W�� `app/build.gradle` �t�@�C���� `dependencies { ... }` �Z�N�V�����ɒǉ����Ă��������B

```groovy
compile "org.jetbrains.kotlinx:kotlinx-coroutines-android:0.16"
```

�R���[�`����Kotlin�̎����I�ȋ@�\�ł��B
`gradle.properties` �t�@�C���Ɏ��̍s��ǉ����邱�ƂŁAKotlin�R���p�C���ŃR���[�`����L���ɂ���K�v������܂��B 
```properties
kotlin.coroutines=enable
```

GitHub��[kotlinx.coroutines](https://github.com/Kotlin/kotlinx.coroutines)�v���W�F�N�g�����[�N�X�e�[�V�����ɃN���[�����邱�Ƃ��ł��܂��B Android�p�̃e���v���[�g�v���W�F�N�g�́A[`ui/kotlinx-coroutines-android/example-app`](kotlinx-coroutines-android/example-app)�f�B���N�g���ɂ���܂��B
Android Studio�œǂݍ����Android�̂��̃K�C�h��ǎ����邱�Ƃ��ł��܂��B

## ��{�I��UI�R���[�`��

���̃Z�N�V�����ł́AUI�A�v���P�[�V�����ł̃R���[�`���̊�{�I�Ȏg�����������܂��B

### UI�R���[�`���̋N��

`kotlinx-coroutines-javafx` ���W���[���ɂ́AJavaFx�A�v���P�[�V�����X���b�h�ɃR���[�`���̎��s���f�B�X�p�b�`����[JavaFx]�R���e�L�X�g���܂܂�Ă��܂��B
�񎦂��ꂽ���ׂĂ̗��Android�ɊȒP�ɈڐA�ł���悤�ɁA����� `UI` �Ƃ��ăC���|�[�g���܂��B
 
```kotlin
import kotlinx.coroutines.experimental.javafx.JavaFx as UI
```
 
<!--- CLEAR -->

UI�X���b�h�Ɍ��肳�ꂽ�R���[�`���́AUI�X���b�h���u���b�N���邱�ƂȂ��AUI���̉��������R�ɍX�V���Ē��f���邱�Ƃ��ł��܂��B
���Ƃ��΁A�A�j���[�V�����𖽗ߓI�ȃX�^�C���ŃR�[�f�B���O���Ď��s���邱�Ƃ��ł��܂��B ���̃R�[�h�́A[launch] �R���[�`���r���_�[���g�p���āA1�b��2��A10����1�ւ̃J�E���g�_�E���Ńe�L�X�g���X�V���܂��B

```kotlin
fun setup(hello: Text, fab: Circle) {
    launch(UI) { // UI�R���e�L�X�g�ŃR���[�`�����N��
        for (i in 10 downTo 1) { // 10����1�܂ŃJ�E���g�_�E��
            hello.text = "Countdown $i ..." // �e�L�X�g���X�V
            delay(500) // 0.5�b�҂�
        }
        hello.text = "Done!"
    }
}
```

> [����](kotlinx-coroutines-javafx/src/test/kotlin/guide/example-ui-basic-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���āA�����N����܂������H
UI�R���e�L�X�g�ŃR���[�`�����N�����Ă���̂ŁA���̃R���[�`��������UI�����R�ɍX�V���A����Ɠ�����[delay]�Ȃǂ̃T�X�y���h�֐����Ăяo�����Ƃ��ł��܂��B
`delay` ���҂��Ă����UI�X���b�h�̓u���b�N����Ȃ��̂�UI�̓t���[�Y���܂���B�����P�ɃR���[�`���𒆒f���܂��B

> Android�A�v���P�[�V�����p�̃R�[�h�������ł��B
`setup` �֐��̖{�̂�Android�v���W�F�N�g�̑Ή�����֐��ɃR�s�[���邾���ł��B

### UI�R���[�`���̃L�����Z��

`launch` �֐����Ԃ�[Job]�I�u�W�F�N�g�ւ̎Q�Ƃ�ێ����A�R���[�`�����L�����Z�����邽�߂Ɏg�����Ƃ��ł��܂��B
�s���N�̉~���N���b�N���ꂽ�Ƃ��ɃR���[�`�����L�����Z�����܂��傤�B

```kotlin
fun setup(hello: Text, fab: Circle) {
    val job = launch(UI) { // UI�R���e�L�X�g�ŃR���[�`�����N��
        for (i in 10 downTo 1) { // 10����1�܂ŃJ�E���g�_�E��
            hello.text = "Countdown $i ..." // �e�L�X�g���X�V
            delay(500) // 0.5�b�҂�
        }
        hello.text = "Done!"
    }
    fab.onMouseClicked = EventHandler { job.cancel() } // �N���b�N���ꂽ��R���[�`�����L�����Z��
}
```

> [����](kotlinx-coroutines-javafx/src/test/kotlin/guide/example-ui-basic-03.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

�J�E���g�_�E�������s����Ă���Ԃɉ~���N���b�N�����ƁA�J�E���g�_�E���͒�~���܂��B
[Job.cancel]�͊��S�ɃX���b�h�Z�[�t�Ńm���u���b�L���O�ł��B
���ۂɏI������̂�҂��ƂȂ��A�R���[�`�������̃W���u���L�����Z������悤�ɒʒm���邾���ł��B �ǂ�����ł��Ăяo�����Ƃ��ł��܂��B
���łɎ�������Ă���A�܂��͊������Ă���R���[�`����ł�����Ăяo���Ă��������܂���B

> Android�̑Ή�����s�͎��̒ʂ�ł��B

```kotlin
fab.setOnClickListener { job.cancel() }  // �N���b�N���ꂽ��R���[�`�����L�����Z��
```

<!--- CLEAR -->

## UI�R���e�L�X�g���ł̃A�N�^�[�̎g�p

���̃Z�N�V�����ł�UI�A�v���P�[�V������UI�R���e�L�X�g���ŃA�N�^�[���ǂ̂悤�Ɏg�p�ł��邩�������A�R���[�`���̋N�����������ɑ������Ă��Ȃ����Ƃ��m�F���܂��B

### �R���[�`���̂��߂̊g��

�������̖ڕW�́A���̊ȒP�ȃR�[�h�ŉ~���N���b�N����邽�тɃJ�E���g�_�E���A�j���[�V���������s�ł���悤�ɁA `onClick`�Ƃ����g���R���[�`���r���_�[�֐����������Ƃł��B

```kotlin
fun setup(hello: Text, fab: Circle) {
    fab.onClick { // �~���N���b�N���ꂽ��R���[�`�����J�n����
        for (i in 10 downTo 1) { // 10����1�܂ŃJ�E���g�_�E��
            hello.text = "Countdown $i ..." // �e�L�X�g���X�V
            delay(500) // 0.5�b�҂�
        }
        hello.text = "Done!"
    }
}
```

<!--- INCLUDE .*/example-ui-actor-([0-9]+).kt -->

`onClick` �̍ŏ��̎����ł́A�e�}�E�X�C�x���g�ŐV�����R���[�`�����N�����A�Ή�����}�E�X�C�x���g���w�肳�ꂽ�A�N�V�����ɓn���܂��i�K�v�ȏꍇ�̂݁j�B

```kotlin
fun Node.onClick(action: suspend (MouseEvent) -> Unit) {
    onMouseClicked = EventHandler { event ->
        launch(UI) {
            action(event)
        }
    }
}
```  

> [����](kotlinx-coroutines-javafx/src/test/kotlin/guide/example-ui-actor-01.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

�~���N���b�N����邽�тɐV�����R���[�`�����n�܂�A���ׂĂ��������ăe�L�X�g���X�V���邱�Ƃɒ��ӂ��Ă��������B
�����Ă݂Ă��������B�ƂĂ��ǂ��Ƃ͎v���܂���B��ŏC�����܂��B

> Android�ł́A�Ή�����g���@�\�� `View` �N���X�p�ɏ������Ƃ��ł���̂ŁA��Ɏ����� `setup` �֐��̃R�[�h��ύX�����Ɏg�����Ƃ��ł��܂��B
Android�ɂ� `MouseEvent` �͂���܂���̂ŏȗ�����Ă��܂��B

```kotlin
fun View.onClick(action: suspend () -> Unit) {
    setOnClickListener { 
        launch(UI) {
            action()
        }
    }
}
```

<!--- CLEAR -->

### �ő��1�̓����W���u

�V�����W���u���J�n����O�ɃA�N�e�B�u�ȃW���u���L�����Z�����邱�ƂŁA�����Ƃ�1�̃R���[�`���������J�E���g�_�E���𓮂����Ă��邱�Ƃ��m���ɂł��܂��B 
�������A����͈�ʓI�ɍŗǂ̃A�C�f�A�ł͂���܂���B
[cancel][Job.cancel]�֐��́A�R���[�`���𒆎~���邽�߂̐M���Ƃ��Ă̂݋@�\���܂��B �L�����Z���͋����I�ł���A�R���[�`���͌����_�ŃL�����Z���s�\�ȉ��������Ă��邩�A�����łȂ���΃L�����Z���M���𖳎����Ă��邩������܂���B ���ǂ�������́A�����Ɏ��s���ׂ��łȂ��^�X�N�ɑ΂���[actor]���g�p���邱�Ƃł��B
`onClick` �g���̎�����ύX���܂��傤�B
  
```kotlin
fun Node.onClick(action: suspend (MouseEvent) -> Unit) {
    // ���̃m�[�h��̂��ׂẴC�x���g����������1�̃A�N�^���N������
    val eventActor = actor<MouseEvent>(UI) {
        for (event in channel) action(event) // �A�N�V�����ɃC�x���g��n��
    }
    // ���̃A�N�^�[�ɃC�x���g��񋟂��郊�X�i�[���C���X�g�[������
    onMouseClicked = EventHandler { event ->
        eventActor.offer(event)
    }
}
```  

> [����](kotlinx-coroutines-javafx/src/test/kotlin/guide/example-ui-actor-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�
  
�A�N�^�[�̃R���[�`���ƒʏ�̃C�x���g�n���h���̓����̍���ɂ���d�v�ȃA�C�f�A�́A[SendChannel]�ɑҋ@���Ȃ�[offer][SendChannel.offer]�֐������邱�Ƃł��B
�\�Ȃ�΃A�N�^�[�ɂ������ɗv�f�𑗐M���A�����łȂ��ꍇ�͗v�f��j�����܂��B
`offer` �͎��ۂɂ͂����ł͖������Ă��� `Boolean` �̌��ʂ�Ԃ��܂��B

���̃o�[�W�����̃R�[�h�ŉ~���J��Ԃ��N���b�N���Ă݂Ă��������B
�J�E���g�_�E���A�j���[�V�����̎��s���́A�N���b�N�͖�������܂��B ����́A�A�N�^�[���A�j���[�V�����ŖZ�����A���̃`���l�������M���Ȃ����߂ɔ������܂��B
�f�t�H���g�ł́A�A�N�^�[�̃��[���{�b�N�X��[RendezvousChannel]�ɂ���Ďx������Ă��܂��B���� `offer` �I�y���[�V�����́A`receive` ���A�N�e�B�u�ȏꍇ�ɂ̂ݐ������܂��B

> Android�ł́A `MouseEvent` �͂���܂���̂ŁA�V�O�i���Ƃ��ăA�N�^�[�� `Unit` �𑗂�܂��B
`View` �N���X�̑Ή�����g���͎��̂悤�ɂȂ�܂��B

```kotlin
fun View.onClick(action: suspend () -> Unit) {
    // 1�̃A�N�^�[���N������
    val eventActor = actor<Unit>(UI) {
        for (event in channel) action()
    }
    // ���̃A�N�^�[���A�N�e�B�u�ɂ��郊�X�i�[���C���X�g�[������
    setOnClickListener { 
        eventActor.offer(Unit)
    }
}
```

<!--- CLEAR -->


### �C�x���g�̍���
 
�ȑO�̃C�x���g���������Ă���ԂɃC�x���g�𖳎�����̂ł͂Ȃ��A�ŐV�̃C�x���g��������������K�؂ȏꍇ������܂��B
[actor]�R���[�`���r���_�[�́A���̃A�N�^�����[���{�b�N�X�Ɏg�p���Ă���`���l���̎����𐧌䂷��A�I�v�V������ `capacity` �p�����[�^���󂯎��܂��B
���p�\�Ȃ��ׂĂ̑I�����̐����́A[Channel()][Channel.invoke]�t�@�N�g���֐��̃h�L�������g�ɋL�ڂ���Ă��܂��B

[Channel.CONFLATED]�̗e�ʒl��n�����Ƃ�[ConflatedChannel]���g�p����R�[�h��ύX���܂��傤�B
���̕ύX�́A�A�N�^���쐬����s�ɂ̂ݓK�p����܂��B

```kotlin
fun Node.onClick(action: suspend (MouseEvent) -> Unit) {
    // ���̃m�[�h��̂��ׂẴC�x���g����������1�̃A�N�^���N������
    val eventActor = actor<MouseEvent>(UI, capacity = Channel.CONFLATED) { // <--- ������ύX
        for (event in channel) action(event) // �C�x���g���A�N�V�����ɓn��
    }
    // ���̃A�N�^�[�ɃC�x���g��񋟂��郊�X�i�[���C���X�g�[������
    onMouseClicked = EventHandler { event ->
        eventActor.offer(event)
    }
}
```  

> [����](kotlinx-coroutines-javafx/src/test/kotlin/guide/example-ui-actor-03.kt)��JavaFx�̊��S�ȃR�[�h���擾�ł��܂�.
Android�ł́A�O�̗�� `val eventActor = ...` �s���X�V����K�v������܂��B

�A�j���[�V�����̎��s���ɃT�[�N�����N���b�N����ƁA�A�j���[�V�����̏I����ɃA�j���[�V��������x�����ĂыN������܂��B
�A�j���[�V�����̎��s���ɌJ��Ԃ��N���b�N�����ƁA_����_ ���čŐV�̃C�x���g�݂̂���������܂��B

����͂܂��A���O�Ɏ�M�����X�V�Ɋ�Â���UI���X�V���邱�Ƃɂ���āA�����Ă��鍂�p�x�̃C�x���g�X�g���[���ɔ������Ȃ���΂Ȃ�Ȃ�UI�A�v���P�[�V�����ɂƂ��Ė]�܂�������ł��B
[ConflatedChannel]���g�p���Ă���R���[�`���́A�C�x���g�̃o�b�t�@�����O�ɂ���đ�������x����h���܂��B

��̍s�� `capacity` �p�����[�^�������āA�R�[�h�̓���ɂǂ̂悤�ɉe�����邩�𒲂ׂ邱�Ƃ��ł��܂��B
`capacity = Channel.UNLIMITED` ��ݒ肷��ƁA���ׂẴC�x���g���o�b�t�@�[����[LinkedListChannel]���[���{�b�N�X�����R���[�`�����쐬����܂��B ���̏ꍇ�A�A�j���[�V�����͉~���N���b�N���ꂽ�񐔂������s����܂��B

## �u���b�L���O����

���̃Z�N�V�����ł́A�X���b�h���u���b�N���鑀���UI�R���[�`�����g�p������@�ɂ��Đ������܂��B

### UI�t���[�Y���

���ׂĂ�API�����s�X���b�h�������ău���b�N���Ȃ��T�X�y���h�֐��Ƃ��ċL�q����Ă���Αf���炵�����Ƃł����B
�������A�قƂ�ǂ̏ꍇ�����ł͂���܂���B �ꍇ�ɂ���ẮA�Ⴆ�ΌĂяo�����X���b�h���u���b�N����ACPU�������v�Z���s������A�l�b�g���[�N�A�N�Z�X�p�̃T�[�h�p�[�e�BAPI���Ăяo�������ł悢�ꍇ������܂��B
����́AUI�X���b�h���u���b�N����UI���t���[�Y���錴���ɂȂ邽�߁AUI�X���b�h��UI����R���[�`�����璼�ڍs�����Ƃ͂ł��܂���B

<!--- INCLUDE .*/example-ui-blocking-([0-9]+).kt

fun Node.onClick(action: suspend (MouseEvent) -> Unit) {
    val eventActor = actor<MouseEvent>(UI, capacity = Channel.CONFLATED) {
        for (event in channel) action(event) // �A�N�V�����ɃC�x���g��n��
    }
    onMouseClicked = EventHandler { event ->
        eventActor.offer(event)
    }
}
-->

���̗�́A���̖��������Ă��܂��B UI�X���b�h�ōŌ�̃N���b�N���������邽�߂ɁA�O�̃Z�N�V������UI�S���̃C�x���g�����A�N�^�[�� `onClick` �g�����g�p���܂��B
���̗�ł́A[�t�B�{�i�b�`��](https://ja.wikipedia.org/wiki/%E3%83%95%E3%82%A3%E3%83%9C%E3%83%8A%E3%83%83%E3%83%81%E6%95%B0)�̑f�p�Ȍv�Z�����s���܂��B
 
```kotlin
fun fib(x: Int): Int =
    if (x <= 1) 1 else fib(x - 1) + fib(x - 2)
``` 
 
�~���N���b�N����邽�тɁA���傫�ȃt�B�{�i�b�`�����v�Z���܂��B
UI�̃t���[�Y����薾�m�ɂ��邽�߂ɁA��Ɏ��s���̍����J�E���g�A�j���[�V����������AUI�R���e�L�X�g�̃e�L�X�g����ɍX�V���Ă��܂��B

```kotlin
fun setup(hello: Text, fab: Circle) {
    var result = "none" // ���O�̌���
    // �J�E���g�A�j���[�V����
    launch(UI) {
        var counter = 0
        while (true) {
            hello.text = "${++counter}: $result"
            delay(100) // 100�~���b���ƂɃe�L�X�g���X�V����
        }
    }
    // �N���b�N���邽�тɎ��̃t�B�{�i�b�`�����v�Z����
    var x = 1
    fab.onClick {
        result = "fib($x) = ${fib(x)}"
        x++
    }
}
```
 
> [����](kotlinx-coroutines-javafx/src/test/kotlin/guide/example-ui-blocking-01.kt)�Ŋ��S��JavaFx�R�[�h���擾�ł��܂��B
`fib` �֐��� `setup` �֐��̖{�̂����Ȃ���Android�v���W�F�N�g�ɃR�s�[���邱�Ƃ��ł��܂��B

���̗�̉~���N���b�N���Ă݂Ă��������B
���悻30�`40��̃N���b�N��A�f�p�Ȍv�Z�͂��Ȃ�x���Ȃ�AUI���t���[�Y���Ă���ԃA�j���[�V��������~����̂�UI�X���b�h���t���[�Y����l�q�������ɂ킩��܂��B

### �u���b�L���O����

UI�X���b�h�ł̃u���b�L���O����̏C���́A�R���[�`���ł͔��ɊȒP�ł��B
"�u���b�N�L���O" `fib` �֐����A[run]�֐����g�p���Ď��s�R���e�L�X�g���o�b�N�O���E���h�X���b�h��[CommonPool]�ɕύX���Čv�Z�����s����A�m���u���b�L���O�T�X�y���h�֐��ɕϊ����܂��B
�܂�A `fib` �֐��� `suspend` �C���q�Ń}�[�N����Ă��܂��B
����́A�Ăяo���ꂽ�R���[�`�����u���b�N���܂��񂪁A�o�b�N�O���E���h�X���b�h�̌v�Z�����삵�Ă���Ƃ��ɂ��̎��s�𒆒f���܂��B

<!--- INCLUDE .*/example-ui-blocking-0[23].kt

fun setup(hello: Text, fab: Circle) {
    var result = "none" // ���O�̌���
    // �J�E���g�A�j���[�V����
    launch(UI) {
        var counter = 0
        while (true) {
            hello.text = "${++counter}: $result"
            delay(100) // 100�~���b���ƂɃe�L�X�g���X�V����
        }
    }
    // �N���b�N���邽�тɎ��̃t�B�{�i�b�`�����v�Z����
    var x = 1
    fab.onClick {
        result = "fib($x) = ${fib(x)}"
        x++
    }
}
-->

```kotlin
suspend fun fib(x: Int): Int = run(CommonPool) {
    if (x <= 1) 1 else fib(x - 1) + fib(x - 2)
}
```

> [����](kotlinx-coroutines-javafx/src/test/kotlin/guide/example-ui-blocking-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂��B

���̃R�[�h�����s���āA�傫�ȃt�B�{�i�b�`�����v�Z����Ă���ԁAUI���t���[�Y���Ă��Ȃ����Ƃ��m�F�ł��܂��B
�������A���̃R�[�h�� `fib` �������炩�x���v�Z���܂��B�Ȃ��Ȃ�A `fib` �ւ̂��ׂĂ̍ċA�Ăяo���� `run` ���o�R���邩��ł��B
����́A���ۂɂ͑傫�Ȗ��ł͂���܂���B�Ȃ��Ȃ�A `run` �̓R���[�`�������łɕK�v�ȃR���e�L�X�g�Ŏ��s����Ă��邩�ǂ������m�F����̂ɏ\���X�}�[�g�ŁA�ʂ̃X���b�h�ɃR���[�`�����ăf�B�X�p�b�`����I�[�o�[�w�b�h������邩��ł��B
����ɂ�������炸�A `run` �̌Ăяo���̊Ԃɐ�����ǉ����鑼�ɉ������Ȃ����̃v���~�e�B�u�R�[�h�ł͖��炩�ɃI�[�o�[�w�b�h������܂��B
�����p�I�ȃR�[�h�ł́A�]���� `run` �Ăяo���̃I�[�o�[�w�b�h�͏d�v�ł͂���܂���B

����ł��A���� `fib` �֐��̖��O�� `fibBlocking` �ɕύX���A `fib` �� `fibBlocking` �̏�� `run` ���b�p�[��킹�Ē�`���ăo�b�N�O���E���h�X���b�h�œ������΁A���� `fib` �̎����͈ȑO�̂悤�ɍ����Ŏ��s�ł��܂��B

```kotlin
suspend fun fib(x: Int): Int = run(CommonPool) {
    fibBlocking(x)
}

fun fibBlocking(x: Int): Int = 
    if (x <= 1) 1 else fibBlocking(x - 1) + fibBlocking(x - 2)
```

> [����](kotlinx-coroutines-javafx/src/test/kotlin/guide/example-ui-blocking-03.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂��B

UI�X���b�h���u���b�N�����ɁA�t���X�s�[�h�̃t�B�{�i�b�`�v�Z���y���ނ��Ƃ��ł��܂��B
�K�v�Ȃ̂́A `run(CommonPool)` �����ł��B

`fib` �֐��̓R�[�h���̒P��̃A�N�^�[����Ăяo�����̂ŁA�^����ꂽ���Ԃɍő�œ�����1�̌v�Z�����邱�Ƃɒ��ӂ��Ă��������B���������āA���̃R�[�h�̓��\�[�X�g�p���Ɏ��R�Ȑ���������܂��B
�ő��1��CPU�R�A��O�a�����邱�Ƃ��ł��܂��B
  
## ���x�ȃg�s�b�N

���̃Z�N�V�����ł́A���܂��܂ȍ��x�ȃg�s�b�N�ɂ��Đ������܂��B
 
### ���C�t�T�C�N���ƃR���[�`���̐e�q�K�w

�T�^�I��UI�A�v���P�[�V�����ɂ́A���C�t�T�C�N���̗v�f������������܂��B
�E�B���h�E�AUI�R���g���[���A�A�N�e�B�r�e�B�A�r���[�A�t���O�����g�A���̑��̎��o�I�v�f���쐬����A�j������܂��B
IO�܂��̓o�b�N�O���E���h�v�Z�����s���钷�����s�R���[�`���́A�K�v�ȏ�ɒ���UI�v�f�ւ̎Q�Ƃ�ێ����A���łɔj������ĕ\������Ȃ�UI�I�u�W�F�N�g�̃c���[�S�̂̃K�x�[�W�R���N�V������j�݂܂��B

���̖��̎��R�ȉ�����́A���C�t�T�C�N�������eUI�I�u�W�F�N�g��[Job]�I�u�W�F�N�g���֘A�t���āA���̃W���u�̃R���e�L�X�g�ł��ׂẴR���[�`�����쐬���邱�Ƃł��B

���Ƃ��΁AAndroid�A�v���P�[�V�����ł͍ŏ��� `Activity` �� _�쐬_ ����A�s�v�ɂȂ����Ƃ��⃁������������Ȃ���΂Ȃ�Ȃ��Ƃ��� _�j��_ ����܂��B
���R�ȉ�����́A `Activity` �̃C���X�^���X�� `Job` �̃C���X�^���X��t�����邱�Ƃł��B
���� `JobHolder` �C���^�t�F�[�X���`���邱�ƂŁA���̂��߂̃~�j�t���[�����[�N���쐬�ł��܂��B

```kotlin
interface JobHolder {
    val job: Job
}
```

�W���u�Ɋ֘A����A�N�e�B�r�e�B�́A���� `JobHolder` �C���^�t�F�[�X���������A�Ή�����W���u���L�����Z�����邽�߂� `onDestroy` �֐����`����K�v������܂��B

```kotlin
class MainActivity : AppCompatActivity(), JobHolder {
    override val job: Job = Job() // ���̃A�N�e�B�r�e�B�̃W���u�C���X�^���X

    override fun onDestroy() {
        super.onDestroy()
        job.cancel() // �A�N�e�B�r�e�B���j�����ꂽ��W���u���L�����Z��
    }
 
    // �c��̃R�[�h
}
```

�܂��A�A�v���P�[�V�������̔C�ӂ̃r���[�̃W���u���擾����֗��ȕ��@���K�v�ł��B
�A�N�e�B�r�e�B�̓r���[��Android `Context`�ł��邽�߁A�ȉ��� `View.contextJob` �g���v���p�e�B���`�ł���̂ŁA����͊ȒP�ł��B

```kotlin
val View.contextJob: Job
    get() = (context as? JobHolder)?.job ?: NonCancellable
```

�����ł́A `contextJob` �g���v���p�e�B���t������W���u�������Ȃ��R���e�L�X�g�ŌĂяo���ꂽ�ꍇ�́A`Job` ��[NonCancellable]�������k���I�u�W�F�N�g�Ƃ��Ďg�p���܂��B

`contextJob` �𗘗p�ł���֗����́A�J�n�����R���[�`���̃��X�g�𖾎��I�Ɉێ����邱�Ƃ�S�z���邱�ƂȂ��A���ׂẴR���[�`�����J�n���邽�߂ɒP���Ɏg�p�ł��邱�Ƃł��B
���ׂẴ��C�t�T�C�N���Ǘ��́A�W���u�Ԃ̐e�q�֌W�̎d�g�݂ɂ���čs���܂��B

�Ⴆ�΁A�O�̃Z�N�V������ `View.onClick` �g���� `contextJob` ���g���Ē�`�ł��܂��B
 
```kotlin
fun View.onClick(action: suspend () -> Unit) {
    // �R���e�L�X�g�W���u��e�Ƃ���1�̃A�N�^�[���N������
    val eventActor = actor<Unit>(contextJob + UI, capacity = Channel.CONFLATED) {
        for (event in channel) action()
    }
    // ���̃A�N�^�[���A�N�e�B�u�ɂ��郊�X�i�[���C���X�g�[������
    setOnClickListener {
        eventActor.offer(Unit)
    }
}
```

��L�̃R�[�h�ŃA�N�^�[���N�����邽�߂� `contextJob + UI` �����ǂ̂悤�Ɏg�p����Ă��邩�ɒ��ڂ��Ă��������B
����́A�W���u�� `UI` �f�B�X�p�b�`���[���܂ސV�����A�N�^�[�̂��߂̃R���[�`���̃R���e�L�X�g���`���܂��B
���� `actor(contextJob + UI)` ���ɂ���ĊJ�n�����R���[�`���́A�Ή�����R���e�L�X�g�̃W���u�̎q�ɂȂ�܂��B
�A�N�e�B�r�e�B���j�����ꂻ�̃W���u���L�����Z�������ƁA���ׂĂ̎q�R���[�`�����L�����Z������܂��B

�W���u�Ԃ̐e�q�֌W�͊K�w���`�����܂��B
�r���[�̑���Ƀo�b�N�O���E���h�W���u�����s����R���[�`���́A���̃R���e�L�X�g�ł���Ȃ�q�R���[�`�������o�����Ƃ��ł��܂��B
�e�W���u���L�����Z�������ƁA�R���[�`���̃c���[�S�̂��L�����Z������܂��B
���̗�́A�R���[�`���̃K�C�h��["�R���[�`���̎q"](../coroutines-guide.md#�R���[�`���̎q)�Z�N�V�����Ɏ�����Ă��܂��B

### �f�B�X�p�b�`������UI�C�x���g�n���h���ŃR���[�`�����J�n����

UI�X���b�h����R���[�`�����N�������Ƃ��̎��s���������o�����邽�߂� `setup` �Ɏ��̃R�[�h�������܂��傤�B

<!--- CLEAR -->

```kotlin
fun setup(hello: Text, fab: Circle) {
    fab.onMouseClicked = EventHandler {
        println("Before launch")
        launch(UI) { 
            println("Inside coroutine")
            delay(100)
            println("After delay")
        } 
        println("After launch")
    }
}
```
 
> [����](kotlinx-coroutines-javafx/src/test/kotlin/guide/example-ui-advanced-01.kt)�Ŋ��S��JavaFx�R�[�h���擾�ł��܂��B

���̃R�[�h���J�n���s���N�̉~���N���b�N����ƁA���̃��b�Z�[�W���R���\�[���ɏo�͂���܂��B
 
```text
Before launch
After launch
Inside coroutine
After delay
```

�����̂悤�ɁA[launch]�̌シ���Ɏ��s���p������A��Ŏ��s���邽�߂ɃR���[�`����UI�X���b�h�Ƀ|�X�g����܂��B
`kotlinx.coroutines` �̂��ׂĂ�UI�f�B�X�p�b�`���͂��̂悤�Ɏ�������Ă��܂��B
�Ȃ��ł��傤���H

��{�I�ɂ����ł̑I���́A�uJS�X�^�C���v�̔񓯊��A�v���[�`�i�񓯊��A�N�V�����͏�Ɍ�œ���̃f�B�X�p�b�`�X���b�h�Ŏ��s�����悤�ɉ�������܂��j�ƁuC#�X�^�C���v�A�v���[�`�i�񓯊��A�N�V�����́A�ŏ��̒��f�|�C���g�܂ŌĂяo�����X���b�h�Ŏ��s����܂��j�̊Ԃł��B

����AC#�̃A�v���[�`�͂������I���Ǝv���܂����A�u�K�v�ȏꍇ�ɂ�`yield`���g���c�v�̂悤�Ȑ��������ŏI���܂��B
����̓G���[���N����₷���ł��B
JS�X�^�C���̃A�v���[�`�͂���ѐ�������A�v���O���}�[��yield����K�v�����邩�ǂ����ɂ��čl����K�v�͂���܂���B

�������A���̓���̃P�[�X�ł́A�R���[�`�����C�x���g�n���h���[����J�n���ꂻ�̂܂��ɑ��̃R�[�h���Ȃ��ꍇ�A���̒ǉ��̃f�B�X�p�b�`�͎��ۂɂ͕t�����l���������]���ȃI�[�o�[�w�b�h��ǉ����܂��B
���̏ꍇ�A[launch]�A[async]�����[actor]�R���[�`���r���_�[�ɑ΂���I�v�V������[CoroutineStart]�p�����[�^���g�p���āA�p�t�H�[�}���X���œK�����邱�Ƃ��ł��܂��B
�����[CoroutineStart.UNDISPATCHED]�̒l�ɐݒ肷��ƁA���̗�Ɏ����悤�ɍŏ��̒��f�|�C���g�܂ł����ɃR���[�`�������s���n�߂���ʂ�����܂��B

```kotlin
fun setup(hello: Text, fab: Circle) {
    fab.onMouseClicked = EventHandler {
        println("Before launch")
        launch(UI, CoroutineStart.UNDISPATCHED) { // <--- ���̕ύX�ɒ���
            println("Inside coroutine")
            delay(100)                            // <--- �����Ă������R���[�`�������f����ꏊ
            println("After delay")
        }
        println("After launch")
    }
}
```
 
> [����](kotlinx-coroutines-javafx/src/test/kotlin/guide/example-ui-advanced-02.kt)�Ŋ��S��JavaFx�R�[�h���擾�ł��܂��B

�N���b�N����Ǝ��̃��b�Z�[�W���v�����g���܂��B�R���[�`���̃R�[�h�̎��s�������ɊJ�n����邱�Ƃ��m�F���Ă��������B

```text
Before launch
Inside coroutine
After launch
After delay
```
  
<!--- MODULE kotlinx-coroutines-core -->
<!--- INDEX kotlinx.coroutines.experimental -->
[launch]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/launch.html
[delay]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/delay.html
[Job]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-job/index.html
[Job.cancel]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-job/cancel.html
[run]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/run.html
[CommonPool]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-common-pool/index.html
[NonCancellable]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-non-cancellable/index.html
[CoroutineStart]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-coroutine-start/index.html
[async]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/async.html
[CoroutineStart.UNDISPATCHED]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-coroutine-start/-u-n-d-i-s-p-a-t-c-h-e-d.html
<!--- INDEX kotlinx.coroutines.experimental.channels -->
[actor]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/actor.html
[SendChannel.offer]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-send-channel/offer.html
[SendChannel]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-send-channel/index.html
[RendezvousChannel]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-rendezvous-channel/index.html
[Channel.invoke]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-channel/invoke.html
[ConflatedChannel]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-conflated-channel/index.html
[Channel.CONFLATED]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-channel/-c-o-n-f-l-a-t-e-d.html
[LinkedListChannel]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-linked-list-channel/index.html
<!--- MODULE kotlinx-coroutines-javafx -->
<!--- INDEX kotlinx.coroutines.experimental.javafx -->
[JavaFx]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-javafx/kotlinx.coroutines.experimental.javafx/-java-fx/index.html
<!--- MODULE kotlinx-coroutines-android -->
<!--- INDEX kotlinx.coroutines.experimental.android -->
<!--- END -->
