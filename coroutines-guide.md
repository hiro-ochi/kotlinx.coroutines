<!--- INCLUDE .*/example-([a-z]+)-([0-9]+)\.kt 
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

// This file was automatically generated from coroutines-guide.md by Knit tool. Do not edit.
package guide.$$1.example$$2

import kotlinx.coroutines.experimental.*
-->
<!--- KNIT     kotlinx-coroutines-core/src/test/kotlin/guide/.*\.kt -->
<!--- TEST_OUT kotlinx-coroutines-core/src/test/kotlin/guide/test/GuideTest.kt
// This file was automatically generated from coroutines-guide.md by Knit tool. Do not edit.
package guide.test

import org.junit.Test

class GuideTest {
--> 

# ����ɂ��kotlinx.coroutines�̎����

����� `kotlinx.coroutines` �̒��j�I�@�\�ɂ��Ă̒Z���K�C�h�ŁA��A�̗�������܂��B

## �����ƃZ�b�g�A�b�v

����Ƃ��Ă�Kotlin�́A���̗l�X�ȃ��C�u�������R���[�`���𗘗p�ł���悤�ɂ��邽�߂ɕW�����C�u�����ɍŏ����̒჌�x��API�����񋟂��Ă��܂���B ���l�̋@�\�������̑����̌���Ƃ͈قȂ�A `async` �� `await` ��Kotlin�̃L�[���[�h�ł͂Ȃ��A�W�����C�u�����̈ꕔ�ł�����܂���B

`kotlinx.coroutines` �͂��̂悤�ȖL�x�ȃ��C�u������1�ł��B����ɂ́Aasync��await���܂ށA���̃K�C�h�ň����������̃R���[�`�����\�ɂ���v���~�e�B�u���܂܂�Ă��܂��B���Ȃ��̃v���W�F�N�g�ł��̃K�C�h�̃v���~�e�B�u���g�p����ɂ́A[����](README.md#in-your-projects)�Ő������� `kotlinx-coroutines-core` ���W���[���Ɉˑ��֌W��ǉ�����K�v������܂��B

## �ڎ�

<!--- TOC -->

* [�R���[�`���̊�b](#�R���[�`���̊�b)
  * [���߂ẴR���[�`��](#���߂ẴR���[�`��)
  * [�u���b�L���O�ƃm���u���b�L���O�̐��E�̋��n��](#�u���b�L���O�ƃm���u���b�L���O�̐��E�̋��n��)
  * [�W���u��҂�](#�W���u��҂�)
  * [�֐����o���t�@�N�^�����O](#�֐����o���t�@�N�^�����O)
  * [�R���[�`���͌y��](#�R���[�`���͌y��)
  * [�R���[�`���̓f�[�����X���b�h�Ɏ��Ă���](#�R���[�`���̓f�[�����X���b�h�Ɏ��Ă���)
* [�L�����Z���ƃ^�C���A�E�g](#�L�����Z���ƃ^�C���A�E�g)
  * [�R���[�`���̎��s���L�����Z��](#�R���[�`���̎��s���L�����Z��)
  * [�L�����Z���͋����I](#�L�����Z���͋����I)
  * [�v�Z�R�[�h���L�����Z���\�ɂ���](#�v�Z�R�[�h���L�����Z���\�ɂ���)
  * [finally�Ń��\�[�X�����](#finally�Ń��\�[�X�����)
  * [�L�����Z���s�u���b�N�̎��s](#�L�����Z���s�u���b�N�̎��s)
  * [�^�C���A�E�g](#�^�C���A�E�g)
* [�T�X�y���h�֐��̍쐬](#�T�X�y���h�֐��̍쐬)
  * [�f�t�H���g�ł̓V�[�P���V����](#�f�t�H���g�ł̓V�[�P���V����)
  * [async���g�p�������񓮍�](#async���g�p�������񓮍�)
  * [�x�����ĊJ�n�����async](#�x�����ĊJ�n�����async)
  * [Async�X�^�C���֐�](#Async�X�^�C���֐�)
* [�R���[�`���R���e�L�X�g�ƃf�B�X�p�b�`���[](#�R���[�`���R���e�L�X�g�ƃf�B�X�p�b�`���[)
  * [�f�B�X�p�b�`���[�ƃX���b�h](#�f�B�X�p�b�`���[�ƃX���b�h)
  * [����Ȃ��ΐ���f�B�X�p�b�`���[](#����Ȃ��ΐ���f�B�X�p�b�`���[)
  * [�R���[�`���ƃX���b�h�̃f�o�b�O](#�R���[�`���ƃX���b�h�̃f�o�b�O)
  * [�X���b�h�Ԃ̃W�����v](#�X���b�h�Ԃ̃W�����v)
  * [�R���e�L�X�g�ɂ�����W���u](#�R���e�L�X�g�ɂ�����W���u)
  * [�R���[�`���̎q](#�R���[�`���̎q)
  * [�R���e�L�X�g�̌���](#�R���e�L�X�g�̌���)
  * [�f�o�b�O�̂��߂̃R���[�`���̖���](#�f�o�b�O�̂��߂̃R���[�`���̖���)
  * [�����I�ȃW���u�ɂ��L�����Z��](#�����I�ȃW���u�ɂ��L�����Z��)
* [�`���l��](#�`���l��)
  * [�`���l���̊�b](#�`���l���̊�b)
  * [�`���l���̃N���[�Y�Ɣ���](#�`���l���̃N���[�Y�Ɣ���)
  * [�`���l���v���f���[�T�[�̍쐬](#�`���l���v���f���[�T�[�̍쐬)
  * [�p�C�v���C��](#�p�C�v���C��)
  * [�p�C�v���C���ɂ��f��](#�p�C�v���C���ɂ��f��)
  * [�_���o�͐�](#�_���o�͐�)
  * [�_�����͐�](#�_�����͐�)
  * [�o�b�t�@�[���ꂽ�`���l��](#�o�b�t�@�[���ꂽ�`���l��)
  * [�`���l���͌���](#�`���l���͌���)
* [���L�~���[�^�u���X�e�[�g�ƕ��s��](#���L�~���[�^�u���X�e�[�g�ƕ��s��)
  * [���](#���)
  * [Volatile�͏����ɂȂ�Ȃ�](#Volatile�͏����ɂȂ�Ȃ�)
  * [�X���b�h�Z�[�t�ȃf�[�^�\��](#�X���b�h�Z�[�t�ȃf�[�^�\��)
  * [�ח��x�̃X���b�h�S��](#�ח��x�̃X���b�h�S��)
  * [�e���x�̃X���b�h�S��](#�e���x�̃X���b�h�S��)
  * [�r������](#�r������)
  * [�A�N�^�[](#�A�N�^�[)
* [�Z���N�g��](#�Z���N�g��)
  * [�`���l������̑I��](#�`���l������̑I��)
  * [�N���[�Y���̑I��](#�N���[�Y���̑I��)
  * [���M�̑I��](#���M�̑I��)
  * [�������ꂽ�l�̑I��](#�������ꂽ�l�̑I��)
  * [�������ꂽ�l�̃`���l���̐؂�ւ�](#�������ꂽ�l�̃`���l���̐؂�ւ�)
* [�Q�l����](#�Q�l����)

<!--- END_TOC -->

## �R���[�`���̊�b

���̃Z�N�V�����ł́A��{�I�ȃR���[�`���̊T�O�ɂ��Đ������܂��B

### ���߂ẴR���[�`��

���̃R�[�h�����s���܂��B

```kotlin
fun main(args: Array<String>) {
    launch(CommonPool) { // ���L�X���b�h�v�[���ɐV�����R���[�`�����쐬����
        delay(1000L) // 1�b�ԃm���u���b�L���O�x�� (�f�t�H���g�̎��ԒP�ʂ�ms)
        println("World!") // delay�̂��ƂŃv�����g
    }
    println("Hello,") // �R���[�`�����x�����Ă���ԁA���C���֐��͌p������
    Thread.sleep(2000L) // ���C���X���b�h��2�b�ԃu���b�N����JVM�𑶑������܂�
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-basic-01.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂��B

���̃R�[�h�����s���܂��B

```text
Hello,
World!
```

<!--- TEST -->

��{�I�ɁA�R���[�`���͌y�ʃX���b�h�ł��B
������[launch] _�R���[�`���r���_�[_ �ŋN�����܂��B
`launch(CommonPool) { ... }` �� `thread { ... }` �ɁA `delay(...)` �� `Thread.sleep(...)` �ɒu�������Ă��������ʂ������܂��B�����Ă݂Ă��������B

`launch(CommonPool)` �� `thread` �ɒu�������ċN������ƁA�R���p�C���͎��̃G���[�𐶐����܂��B

```
Error: Kotlin: �T�X�y���h�֐��́A�R���[�`���܂��͑��̃T�X�y���h�֐�����̂݌Ăяo�����Ƃ��ł��܂�
```

����́A [delay] ���X���b�h���u���b�N�����A�R���[�`���� _���f_ ���R���[�`������̂ݎg�p�ł�����ʂ� _�T�X�y���h�֐�_ �ł��邽�߂ł��B

### �u���b�L���O�ƃm���u���b�L���O�̐��E�̋��n��

�ŏ��̗�ł́A `main` �֐��̓����R�[�h���ɁA_�m���u���b�L���O_ `delay(...)` �� _�u���b�L���O_ `Thread.sleep(...)` �����݂����Ă��܂��B
���q�ɂȂ�̂͊ȒP�ł��B
[runBlocking]���g�p���āA�u���b�L���O�ƃm���u���b�L���O�̐��E�����ꂢ�ɕ������܂��傤�B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> { // ���C���R���[�`�����J�n
    launch(CommonPool) { // ���L�X���b�h�v�[���ɐV�����R���[�`�����쐬����
        delay(1000L)
        println("World!")
    }
    println("Hello,") // �q���x�����Ă���ԃ��C���R���[�`���͌p������
    delay(2000L) // 2�b�ԃm���u���b�L���O�x������JVM�𑶑�������
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-basic-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂��B

<!--- TEST
Hello,
World!
-->

���ʂ͓����ł����A���̃R�[�h�ł̓m���u���b�L���O[delay]�݂̂��g�p���Ă��܂��B

`runBlocking { ... }` �́A�g�b�v���x���̃��C���R���[�`�����N�����邽�߂ɂ����Ŏg�p�����A�_�v�^�Ƃ��ċ@�\���܂��B
`runBlocking` �̊O���̒ʏ�̃R�[�h�́A `runBlocking` �����̃R���[�`�����A�N�e�B�u�ɂȂ�܂� _�u���b�N_ ���܂��B

����͂܂��A�T�X�y���h�֐��̒P�̃e�X�g���������@�ł�����܂��B
 
```kotlin
class MyTest {
    @Test
    fun testMySuspendingFunction() = runBlocking<Unit> {
        // �����ł́A�D���ȃA�T�[�V�����X�^�C�����g���ăT�X�y���h�֐����g�����Ƃ��ł��܂�
    }
}
```

<!--- CLEAR -->
 
### �W���u��҂�

�ʂ̃R���[�`�������삵�Ă���Ԓx��������̂͗ǂ����@�ł͂���܂���B
�����グ���o�b�N�O���E���h[Job]����������܂Ŗ����I�Ɂi�m���u���b�L���O�̕��@�Łj�҂��܂��傤�B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val job = launch(CommonPool) { // �V�����R���[�`�����쐬���A����Job�ւ̎Q�Ƃ�ێ�����
        delay(1000L)
        println("World!")
    }
    println("Hello,")
    job.join() // �q�R���[�`������������܂ő҂�
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-basic-03.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂��B

<!--- TEST
Hello,
World!
-->

���ʂ͕ς��܂��񂪁A���C���R���[�`���̃R�[�h�̓o�b�N�O���E���h�W���u�̌p�����ԂɌ��т��Ă��܂���B�����Ɨǂ��ł��B

### �֐����o���t�@�N�^�����O

`launch(CommonPool) { ... }` �̒��̃R�[�h�u���b�N��ʂ̊֐��ɒ��o���܂��傤�B
���̃R�[�h�� "Extract function"���t�@�N�^�����O�����s����ƁA `suspend` �C���q�t���̐V�����֐��������܂��B
���ꂪ���Ȃ��̍ŏ��� _�T�X�y���h�֐�_ �ł��B
�T�X�y���h�֐��́A�ʏ�̊֐��Ɠ��l�ɃR���[�`�����Ŏg�p�ł��܂����A�ǉ��@�\�Ƃ��āA���̗�ł� `delay`�̂悤�ȑ��̃T�X�y���h�֐����g�p���ăR���[�`���̎��s�� _���f_ ���邱�Ƃ��ł��܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val job = launch(CommonPool) { doWorld() }
    println("Hello,")
    job.join()
}

// ����͂��Ȃ��̍ŏ��̃T�X�y���h�֐�
suspend fun doWorld() {
    delay(1000L)
    println("World!")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-basic-04.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST
Hello,
World!
-->

### �R���[�`���͌y��

���̃R�[�h�����s���܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val jobs = List(100_000) { // �R���[�`��������������A�W���u�����X�g����
        launch(CommonPool) {
            delay(1000L)
            print(".")
        }
    }
    jobs.forEach { it.join() } // ���ׂẴW���u����������̂�҂�
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-basic-05.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST lines.size == 1 && lines[0] == ".".repeat(100_000) -->

10���̃R���[�`�����J�n���A1����Ɋe�R���[�`�����h�b�g���v�����g���܂��B
�X���b�h���g���Ď�������ǂ��Ȃ�ł��傤���H �i�قƂ�ǂ̏ꍇ�A���Ȃ��̃R�[�h�̓������s���G���[�������N�����ł��傤�j

### �R���[�`���̓f�[�����X���b�h�Ɏ��Ă���

���̃R�[�h�ł́A�uI'm sleeping�v�Ƃ������b�Z�[�W�𖈕b2��o�͂��A���ɂ�����x�x���main�֐����烊�^�[�����钷�����s�̃R���[�`�����N�����܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    launch(CommonPool) {
        repeat(1000) { i ->
            println("I'm sleeping $i ...")
            delay(500L)
        }
    }
    delay(1300L) // �x��ďI������
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-basic-06.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���s����ƁA3�s���o�͂��ďI�����邱�Ƃ��킩��܂��B

```text
I'm sleeping 0 ...
I'm sleeping 1 ...
I'm sleeping 2 ...
```

<!--- TEST -->

�A�N�e�B�u�ȃR���[�`���̓v���Z�X�𐶂���������킯�ł͂���܂���B�����̓f�[�����X���b�h�̂悤�Ȃ��̂ł��B

## �L�����Z���ƃ^�C���A�E�g

���̃Z�N�V�����ł́A�R���[�`���̃L�����Z���ƃ^�C���A�E�g�ɂ��Đ������܂��B

### �R���[�`���̎��s���L�����Z��

�����ȃA�v���P�[�V�����ł́A"main"���\�b�h����̃��^�[���́A�ÖٓI�ɂ��ׂẴR���[�`�����I��������ǂ��l���̂悤�Ɏv���邩������܂���B
��K�͂Œ����Ԏ��s�����A�v���P�[�V�����ł́A���ߍׂ��Ȑ��䂪�K�v�ł��B
[launch]�֐��́A���s���̃R���[�`�������������߂Ɏg�p�ł���[job]��Ԃ��܂��B
 
```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val job = launch(CommonPool) {
        repeat(1000) { i ->
            println("I'm sleeping $i ...")
            delay(500L)
        }
    }
    delay(1300L) // �����x�点��
    println("main: I'm tired of waiting!")
    job.cancel() // �W���u���L�����Z��
    delay(1300L) // �{���ɃL�����Z�����ꂽ���Ƃ��m�F���邽�߂ɏ����x�点��
    println("main: Now I can quit.")
}
``` 

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-cancel-01.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̏o�͂���������܂��B

```text
I'm sleeping 0 ...
I'm sleeping 1 ...
I'm sleeping 2 ...
main: I'm tired of waiting!
main: Now I can quit.
```

<!--- TEST -->

���C���� `job.cancel` ���Ăяo���Ƃ����ɃL�����Z������邽�ߑ��̃R���[�`������̏o�͕͂\������܂���B

### �L�����Z���͋����I

�R���[�`���̃L�����Z���� _�����I_ �ł��B�R���[�`���R�[�h�͎������\�ɂ��邽�߂ɋ������Ȃ���΂Ȃ�܂���B
`kotlinx.coroutines` �̃T�X�y���h�֐��͂��ׂ� _�L�����Z���\_ �ł��B
�����̓R���[�`���̃L�����Z�����`�F�b�N���A�L�����Z�������[CancellationException]���X���[���܂��B
�������A�R���[�`�����v�Z�ō�Ƃ��Ă��Ď��������`�F�b�N���Ă��Ȃ��ꍇ�A���̗�̂悤�Ɏ��������Ƃ͂ł��܂���B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val job = launch(CommonPool) {
        var nextPrintTime = 0L
        var i = 0
        while (i < 10) { // �v�Z���[�v
            val currentTime = System.currentTimeMillis()
            if (currentTime >= nextPrintTime) {
                println("I'm sleeping ${i++} ...")
                nextPrintTime = currentTime + 500L
            }
        }
    }
    delay(1300L) // �����x�点��
    println("main: I'm tired of waiting!")
    job.cancel() // �W���u���L�����Z��
    delay(1300L) // �L�����Z�����ꂽ���ǂ����m���߂邽�߂ɏ����x�点��c
    println("main: Now I can quit.")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-cancel-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���s���āA�L�����Z����� "I'm sleeping" �ƃv�����g�������邱�Ƃ��m�F���܂��B

<!--- TEST 
I'm sleeping 0 ...
I'm sleeping 1 ...
I'm sleeping 2 ...
main: I'm tired of waiting!
I'm sleeping 3 ...
I'm sleeping 4 ...
I'm sleeping 5 ...
main: Now I can quit.
-->

### �v�Z�R�[�h���L�����Z���\�ɂ���

�v�Z�R�[�h���L�����Z���\�ɂ���ɂ�2�̕��@������܂��B
1�́A����I�ɃT�X�y���h�֐����Ăяo�����Ƃł��B
���̖ړI�̂��߂ɗǂ��I�����ł���[yield]�֐�������܂��B
����1�́A�L�����Z���X�e�[�^�X�𖾎��I�Ƀ`�F�b�N���邱�Ƃł��B��҂̕��@�������Ă݂܂��傤�B

�O�̗�� `while (true)` �� `while (isActive)` �ɒu�������čĎ��s���Ă��������B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val job = launch(CommonPool) {
        var nextPrintTime = 0L
        var i = 0
        while (isActive) { // �L�����Z���\�Ȍv�Z���[�v
            val currentTime = System.currentTimeMillis()
            if (currentTime >= nextPrintTime) {
                println("I'm sleeping ${i++} ...")
                nextPrintTime = currentTime + 500L
            }
        }
    }
    delay(1300L) // �����x�点��
    println("main: I'm tired of waiting!")
    job.cancel() // �W���u���L�����Z��
    delay(1300L) // �L�����Z�����ꂽ���ǂ����m���߂邽�߂ɏ����x�点��c
    println("main: Now I can quit.")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-cancel-03.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

�����̂Ƃ���A���̃��[�v�̓L�����Z���ł��܂��B
[isActive][CoroutineScope.isActive]�́A[CoroutineScope]�I�u�W�F�N�g����ăR���[�`���̃R�[�h���Ŏg�p�ł���v���p�e�B�ł��B

<!--- TEST
I'm sleeping 0 ...
I'm sleeping 1 ...
I'm sleeping 2 ...
main: I'm tired of waiting!
main: Now I can quit.
-->

### finally�Ń��\�[�X�����

�L�����Z���\�ȃT�X�y���h�֐��́A�L�����Z���̍ۂɒʏ�̕��@�ŏ����ł���CancellationException���X���[���܂��B
���Ƃ��΁A `try {...} finally {...}` ��Kotlin `use` �֐��́A�R���[�`�����L�����Z�����ꂽ�Ƃ��ɁA�ʏ�̏I�����������s���܂��B
 
```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val job = launch(CommonPool) {
        try {
            repeat(1000) { i ->
                println("I'm sleeping $i ...")
                delay(500L)
            }
        } finally {
            println("I'm running finally")
        }
    }
    delay(1300L) // �����x�点��
    println("main: I'm tired of waiting!")
    job.cancel() // �W���u���L�����Z��
    delay(1300L) // �{���ɃL�����Z�����ꂽ���Ƃ��m�F���邽�߂ɏ����x�点��
    println("main: Now I can quit.")
}
``` 

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-cancel-04.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̗�͎��̏o�͂𐶐����܂��B

```text
I'm sleeping 0 ...
I'm sleeping 1 ...
I'm sleeping 2 ...
main: I'm tired of waiting!
I'm running finally
main: Now I can quit.
```

<!--- TEST -->

### �L�����Z���s�u���b�N�̎��s

�O�̗�� `finally` �u���b�N�ŃT�X�y���h�֐����g�p���悤�Ƃ���ƁA���̃R�[�h�����s���Ă���R���[�`�����L�����Z������邽��[CancellationException]���������܂��B
�i�t�@�C�������A�W���u���L�����Z������A�܂��͂������ނ̒ʐM�`���l�������Ȃǁj����ɓ��삷�邷�ׂẴN���[�Y����͑��m���u���b�L���O�ł���A�T�X�y���h�֐��͊܂܂�Ȃ����߁A�ʏ킱��͖��ł͂���܂���B
�������A�L�����Z�����ꂽ�R���[�`���Œ��f����K�v������܂�ȃP�[�X�ł́A���̗�̂悤�� [run]�֐��� [NonCancellable]�R���e�L�X�g���g�p���� `run(NonCancellable) {...}` �ɑΉ�����R�[�h�����b�v���邱�Ƃ��ł��܂��B
 
```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val job = launch(CommonPool) {
        try {
            repeat(1000) { i ->
                println("I'm sleeping $i ...")
                delay(500L)
            }
        } finally {
            run(NonCancellable) {
                println("I'm running finally")
                delay(1000L)
                println("And I've just delayed for 1 sec because I'm non-cancellable")
            }
        }
    }
    delay(1300L) // delay a bit
    println("main: I'm tired of waiting!")
    job.cancel() // cancels the job
    delay(1300L) // delay a bit to ensure it was cancelled indeed
    println("main: Now I can quit.")
}
``` 

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-cancel-05.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST
I'm sleeping 0 ...
I'm sleeping 1 ...
I'm sleeping 2 ...
main: I'm tired of waiting!
I'm running finally
And I've just delayed for 1 sec because I'm non-cancellable
main: Now I can quit.
-->

### �^�C���A�E�g

�R���[�`���̎��s�����ۂɃL�����Z������ł������ȗ��R�́A���̎��s���Ԃ��^�C���A�E�g�𒴂������߂ł��B
�Ή�����[Job]�ւ̎Q�Ƃ��蓮�ŒǐՂ��A�x���̌�ŒǐՂ��ꂽ���̂����������߂ɕʂ̃R���[�`�����N�����邱�Ƃ͂ł��܂����A������s��[withTimeout]�֐����p�ӂ���Ă��܂��B
���̗�����Ă��������B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    withTimeout(1300L) {
        repeat(1000) { i ->
            println("I'm sleeping $i ...")
            delay(500L)
        }
    }
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-cancel-06.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

����͎��̏o�͂𐶐����܂��B

```text
I'm sleeping 0 ...
I'm sleeping 1 ...
I'm sleeping 2 ...
Exception in thread "main" kotlinx.coroutines.experimental.TimeoutException: Timed out waiting for 1300 MILLISECONDS
```

<!--- TEST STARTS_WITH -->

[withTimeout]�ɂ���ăX���[����� `TimeoutException` �́A[CancellationException]�̃v���C�x�[�g�T�u�N���X�ł��B
��̃R���\�[���ɂ̓X�^�b�N�g���[�X���\������Ă��܂���ł����B
�L�����Z�����ꂽ�R���[�`������ `CancellationException` ���R���[�`�������̒ʏ�̗��R�ł���ƍl�����邽�߂ł��B
�������A���̗�ł� `main` �֐��̒��� `withTimeout` ���g�p���Ă��܂��B

�L�����Z���͒P�Ȃ��O�Ȃ̂ŁA���ׂẴ��\�[�X�͒ʏ�̕��@�ŕ����܂��B
�^�C���A�E�g���ɓ��ʂȃA�N�V������ǉ�����K�v������ꍇ�́A `try {...} catch (e�FCancellationException) {...}` �u���b�N�Ń^�C���A�E�g���g�����R�[�h�����b�v���邱�Ƃ��ł��܂��B

## �T�X�y���h�֐��̍쐬

���̃Z�N�V�����ł́A�T�X�y���h�֐��̂��܂��܂ȍ\�����@�ɂ��Đ������܂��B

### �f�t�H���g�ł̓V�[�P���V����

���炩�̃����[�g�T�[�r�X�R�[����v�Z�̂悤�ɗL�p�ȉ������s�����̏ꏊ�Œ�`���ꂽ2�̃T�X�y���h�֐�������Ƃ��܂��B ���ۂɂ͂��̗�̖ړI�̂��߂ɂ��ꂼ�ꂽ��1�b�x�点�邾���ł����A�����͗L�p�Ȃ��̂Ƃ��Ă����܂��B

<!--- INCLUDE .*/example-compose-([0-9]+).kt
import kotlin.system.measureTimeMillis
-->

```kotlin
suspend fun doSomethingUsefulOne(): Int {
    delay(1000L) // �����L�p�Ȃ��Ƃ����Ă���ӂ�
    return 13
}

suspend fun doSomethingUsefulTwo(): Int {
    delay(1000L) // ������A�����L�p�Ȃ��Ƃ����Ă���ӂ�
    return 29
}
```

<!--- INCLUDE .*/example-compose-([0-9]+).kt -->

�ŏ��� `doSomethingUsefulOne` �����s���Ă��� `doSomethingUsefulTwo` �����s���A���̌��ʂ̍��v���v�Z���܂��B����� _�A������_ �Ăяo���K�v������ꍇ�͂ǂ�����΂悢�ł����B
���ۂɂ́A��1�̊֐��̌��ʂ��g�p���āA��2�̊֐����Ăяo���K�v�����邩�ǂ����A���邢�͌Ăяo�����@�����肷�邽�߂ɁA������s���܂��B

�R���[�`���̃R�[�h�͒ʏ�̃R�[�h�Ɠ��l�Ƀf�t�H���g�ł� _�V�[�P���V����_ �Ȃ̂ŁA�ʏ�̏����Ăяo�����g�p���܂��B
���̗�́A�����̃T�X�y���h�֐������s����̂ɂ����鍇�v���Ԃ𑪒肷�邱�Ƃɂ���Ă���������Ă��܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val time = measureTimeMillis {
        val one = doSomethingUsefulOne()
        val two = doSomethingUsefulTwo()
        println("The answer is ${one + two}")
    }
    println("Completed in $time ms")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-compose-01.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

����͎��̂悤�ȏo�͂����܂��B

```text
The answer is 42
Completed in 2017 ms
```

<!--- TEST FLEXIBLE_TIME -->

### async���g�p�������񓮍�

`doSomethingUsefulOne` �� `doSomethingUsefulTwo` �̌Ăяo���̊ԂɈˑ��֌W���Ȃ��A������ _����_ �ɍs�����Ƃł�葬���������o�������̂ł����H
�����[async]�������ɂȂ��ʂł��B

�T�O�I�ɂ́A[async]��[launch]�Ɠ����ł��B
����͕ʂ̃R���[�`�����J�n���܂��B���̃R���[�`���́A���̂��ׂẴR���[�`���Ɠ����ɓ��삷��y�ʃX���b�h�ł��B
����_�� `launch` ��[Job]��Ԃ��A���ʂ̒l�͎����܂��񂪁A `async` �͌��ʂ���Œ񋟂���񑩂�\���y�ʂŃm���u���b�L���O�ȃt���[�`���[�ł���[Deferred]��Ԃ��܂��B
�x�����ꂽ�l�ɑ΂��� `.await()` ���g�p���čŏI�I�Ȍ��ʂ𓾂邱�Ƃ��ł��܂����A `Deferred` �� `Job` �Ȃ̂ŕK�v�ɉ����ăL�����Z�����邱�Ƃ��ł��܂��B
 
```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val time = measureTimeMillis {
        val one = async(CommonPool) { doSomethingUsefulOne() }
        val two = async(CommonPool) { doSomethingUsefulTwo() }
        println("The answer is ${one.await() + two.await()}")
    }
    println("Completed in $time ms")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-compose-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̂悤�Ȃ��̂���������܂��B

```text
The answer is 42
Completed in 1017 ms
```

<!--- TEST FLEXIBLE_TIME -->

2�̃R���[�`���������Ɏ��s����邽�߁A�����2�{�����ł��B
�R���[�`���̕��s���͏�ɖ����I�ł��邱�Ƃɒ��ӂ��Ă��������B

### �x�����ĊJ�n�����async

[CoroutineStart.LAZY]�p�����[�^���g�p����[async]�ɂ��邽�߂̒x���I�v�V����������܂��B
�R���[�`���́A [await][Deferred.await]�܂��� [start][Job.start]�֐����Ăяo���ꂽ�Ƃ��ɂ��̌��ʂ��K�v�ȏꍇ�ɂ̂݊J�n����܂��B
�O�̗�Ƃ��̃I�v�V�����������قȂ鎟�̗�����s���܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val time = measureTimeMillis {
        val one = async(CommonPool, CoroutineStart.LAZY) { doSomethingUsefulOne() }
        val two = async(CommonPool, CoroutineStart.LAZY) { doSomethingUsefulTwo() }
        println("The answer is ${one.await() + two.await()}")
    }
    println("Completed in $time ms")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-compose-03.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̂悤�Ȃ��̂���������܂��B

```text
The answer is 42
Completed in 2017 ms
```

<!--- TEST FLEXIBLE_TIME -->

�Ȃ�ƁA�V�[�P���V�����Ȏ��s�ɖ߂��Ă��܂��܂����B����́A�ŏ��� `one` ���J�n���đ҂��Ă���A`two` ���J�n���đ҂��߂ł��B
�x���ɂƂ��ĈӐ}���ꂽ���[�X�P�[�X�ł͂���܂���B
����͒l�̌v�Z�ɃT�X�y���h�֐����܂܂��Ƃ��ɁA�W���� `lazy` �֐��ɑ�����̂Ƃ��Đ݌v����Ă��܂��B

### Async�X�^�C���֐�

[async]�R���[�`���r���_�[���g�p���� _�񓯊��I_ �� `doSomethingUsefulOne` �� `doSomethingUsefulTwo` ���Ăяo��async�X�^�C���̊֐����`�ł��܂��B
"async"�ړ�����"Async"�ڔ�����t���āA��ɔ񓯊��Ōv�Z���J�n���A���̌��ʓ�����x���l���g�p����K�v������Ƃ����������������邽�߂ɁA���̂悤�Ȋ֐��̖��O��t���邱�Ƃ͗ǂ��X�^�C���ł��B

```kotlin
// The result type of asyncSomethingUsefulOne is Deferred<Int>
fun asyncSomethingUsefulOne() = async(CommonPool) {
    doSomethingUsefulOne()
}

// The result type of asyncSomethingUsefulTwo is Deferred<Int>
fun asyncSomethingUsefulTwo() = async(CommonPool)  {
    doSomethingUsefulTwo()
}
```

������ `asyncXXX` �֐��́A_�T�X�y���h_ �֐�**�ł͂Ȃ�**���Ƃɒ��ӂ��Ă��������B
�����͂ǂ�����ł��g�p�ł��܂��B
�������A�Ăяo���R�[�h�̃A�N�V�����͏�ɔ񓯊��i�����ł� _���s���s_ ���Ӗ�����j���s�ł��邱�ƈӖ����܂��B

���̗�́A�R���[�`���̊O���ł̎g�p��������Ă��܂��B
 
```kotlin
// ���̗�ł́A `main` �̉E���� `runBlocking` ���Ȃ����Ƃɒ��ӂ��Ă�������
fun main(args: Array<String>) {
    val time = measureTimeMillis {
        // we can initiate async actions outside of a coroutine
        val one = asyncSomethingUsefulOne()
        val two = asyncSomethingUsefulTwo()
        // but waiting for a result must involve either suspending or blocking.
        // here we use `runBlocking { ... }` to block the main thread while waiting for the result
        runBlocking {
            println("The answer is ${one.await() + two.await()}")
        }
    }
    println("Completed in $time ms")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-compose-04.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST FLEXIBLE_TIME
The answer is 42
Completed in 1085 ms
-->

## �R���[�`���R���e�L�X�g�ƃf�B�X�p�b�`���[

�������͂��ł� `launch(CommonPool) {...}` �A `async(CommonPool) {...}` �A `run(NonCancellable) {...}` �Ȃǂ����Ă��܂����B
�����̃R�[�h�X�j�y�b�g[CommonPool]��[NonCancellable]�� _�R���[�`���R���e�L�X�g_ �ł��B
���̃Z�N�V�����ł́A���̑��̑I�����ɂ��Đ������܂��B

### �f�B�X�p�b�`���[�ƃX���b�h

�R���[�`���R���e�L�X�g�ɂ́A[_�R���[�`���f�B�X�p�b�`��_][CoroutineDispatcher]���܂܂�Ă���A�Ή�����R���[�`�������s�Ɏg�p����X���b�h�i�P�Ƃ܂��͕����j�����肵�܂��B�R���[�`���f�B�X�p�b�`���́A�R���[�`���̎��s�����̃X���b�h�Ɍ��肵����A�X���b�h�v�[���Ƀf�B�X�p�b�`������A����Ȃ��Ŏ��s�������肷�邱�Ƃ��ł��܂��B ���̗�������Ă��������B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val jobs = arrayListOf<Job>()
    jobs += launch(Unconfined) { // ����Ȃ� -- ���C���X���b�h�œ��삷��
        println(" 'Unconfined': I'm working in thread ${Thread.currentThread().name}")
    }
    jobs += launch(context) { // �e(runBlocking�R���[�`��)�̃R���e�L�X�g
        println("    'context': I'm working in thread ${Thread.currentThread().name}")
    }
    jobs += launch(CommonPool) { // ForkJoinPool.commonPool(�܂��͓��l�Ȃ���)�Ƀf�B�X�p�b�`�����
        println(" 'CommonPool': I'm working in thread ${Thread.currentThread().name}")
    }
    jobs += launch(newSingleThreadContext("MyOwnThread")) { // �Ǝ��̐V�����X���b�h���擾
        println("     'newSTC': I'm working in thread ${Thread.currentThread().name}")
    }
    jobs.forEach { it.join() }
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-context-01.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̏o�͂𐶐����܂��i�����炭�قȂ鏇���Łj�B

```text
 'Unconfined': I'm working in thread main
 'CommonPool': I'm working in thread ForkJoinPool.commonPool-worker-1
     'newSTC': I'm working in thread MyOwnThread
    'context': I'm working in thread main
```

<!--- TEST LINES_START_UNORDERED -->

The difference between parent [context][CoroutineScope.context] and [Unconfined] context will be shown later.

�e[�R���e�L�X�g][CoroutineScope.context]��[Unconfined]�R���e�L�X�g�̈Ⴂ�ɂ��ẮA��Ő������܂��B

### ����Ȃ��ΐ���f�B�X�p�b�`���[
 
[Unconfined]�R���[�`���f�B�X�p�b�`���́A�ŏ��̒��f�|�C���g�܂ŌĂяo�����X���b�h�ŃR���[�`���Ŏ��s���܂��B
���f��A�Ăяo���ꂽ�T�X�y���h�֐��ɂ���Ċ��S�Ɍ��肳�ꂽ�X���b�h�ōĊJ����܂��B
�R���[�`����CPU���Ԃ�����Ȃ��ꍇ��A����̃X���b�h�Ɍ��肳�ꂽ���L�f�[�^�iUI�Ȃǁj���X�V���Ȃ��ꍇ�AUnconfined�f�B�X�p�b�`�����K�؂ł��B

����A[CoroutineScope]�C���^�[�t�F�C�X����ăR���[�`���̃u���b�N���Ŏg�p�ł���[�R���e�L�X�g][CoroutineScope.context]�v���p�e�B�́A���̓���̃R���[�`���̃R���e�L�X�g�ւ̎Q�Ƃł��B
���̂悤�ɂ��āA�e�R���e�L�X�g���p�����邱�Ƃ��ł��܂��B
���ɁA[runBlocking]�̃f�t�H���g�R���e�L�X�g�͌Ăяo�����X���b�h�Ɍ��肳��Ă��邽�߁A�p������Ɨ\���\��FIFO�X�P�W���[�����O���g�p���Ă��̃X���b�h�Ɏ��s�����肷��Ƃ������ʂ�����܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val jobs = arrayListOf<Job>()
    jobs += launch(Unconfined) { // ����Ȃ� -- ���C���X���b�h�œ��삷��
        println(" 'Unconfined': I'm working in thread ${Thread.currentThread().name}")
        delay(500)
        println(" 'Unconfined': After delay in thread ${Thread.currentThread().name}")
    }
    jobs += launch(context) { // �e(runBlocking�R���[�`��)�̃R���e�L�X�g
        println("    'context': I'm working in thread ${Thread.currentThread().name}")
        delay(1000)
        println("    'context': After delay in thread ${Thread.currentThread().name}")
    }
    jobs.forEach { it.join() }
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-context-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̂悤�ɏo�͂��܂��B
 
```text
 'Unconfined': I'm working in thread main
    'context': I'm working in thread main
 'Unconfined': After delay in thread kotlinx.coroutines.ScheduledExecutor
    'context': After delay in thread main
```

<!--- TEST LINES_START -->
 
���̂悤�ɁA `runBlocking {...}` �R���[�`���� `context` ���p�������R���[�`���� `main` �X���b�h�Ŏ��s�������܂����A����Ȃ��̂ق��̓X���b�h��[delay]�֐����g�p���Ă���X�P�W���[���X���b�h�ōĊJ���܂����B

### �R���[�`���ƃX���b�h�̃f�o�b�O

�R���[�`���́A[Unconfined]�f�B�X�p�b�`���܂���[CommonPool]�̂悤�ȃ}���`�X���b�h�f�B�X�p�b�`�����g�p���āA����X���b�h�Œ��f���A�ʂ̃X���b�h�ōĊJ�ł��܂��B
�V���O���X���b�h�̃f�B�X�p�b�`���ł����Ă��A�R���[�`���������A���A�ǂ��ł���Ă����̂��c������͓̂����������܂���B
�X���b�h���g�p���ăA�v���P�[�V�������f�o�b�O�����ʓI�ȕ��@�́A���O�t�@�C���̊e���O�X�e�[�g�����g�ɃX���b�h�����o�͂��邱�Ƃł��B
���̋@�\�́A���M���O�t���[�����[�N�ɂ���ĕ��ՓI�ɃT�|�[�g����Ă��܂��B �R���[�`�����g�p����ꍇ�A�X���b�h�������ł̓R���e�L�X�g�̑����������Ȃ��̂ŁA `kotlinx.coroutines`�ɂ̓f�o�b�O�@�\���g�ݍ��܂�Ă��܂��B

`-Dkotlinx.coroutines.debug` JVM�I�v�V������t���Ď��̃R�[�h�����s���Ă��������B

```kotlin
fun log(msg: String) = println("[${Thread.currentThread().name}] $msg")

fun main(args: Array<String>) = runBlocking<Unit> {
    val a = async(context) {
        log("I'm computing a piece of the answer")
        6
    }
    val b = async(context) {
        log("I'm computing another piece of the answer")
        7
    }
    log("The answer is ${a.await() * b.await()}")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-context-03.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

`runBlocking` �̃��C���R���[�`���i#1�j�ƁA�x���l���v�Z����2�̃R���[�`�� `a` �i#2�j�ƁA`b` �i#3�j��3�̃R���[�`��������܂��B
�����͂��ׂ� `runBlocking` �̃R���e�L�X�g�Ŏ��s����Ă���A���C���X���b�h�Ɍ��肳��Ă��܂��B
���̃R�[�h�̏o�͎͂��̂Ƃ���ł��B

```text
[main @coroutine#2] I'm computing a piece of the answer
[main @coroutine#3] I'm computing another piece of the answer
[main @coroutine#1] The answer is 42
```

<!--- TEST -->

`log` �֐��̓X���b�h�̖��O���p���ʂŃv�����g���A`main` �X���b�h�ł��邱�Ƃ��킩��܂����A���ݎ��s���̃R���[�`���̎��ʎq���ǉ�����Ă��܂��B
���̎��ʎq�́A�f�o�b�O���[�h���I���̂Ƃ��ɁA�쐬���ꂽ���ׂẴR���[�`���ɘA�����Ċ��蓖�Ă��܂��B

�f�o�b�O�@�\�̏ڍׂɂ��ẮA[newCoroutineContext]�֐��̃h�L�������g���Q�Ƃ��Ă��������B

### �X���b�h�Ԃ̃W�����v

`-Dkotlinx.coroutines.debug` JVM�I�v�V�����Ŏ��̃R�[�h�����s���Ă��������B

```kotlin
fun log(msg: String) = println("[${Thread.currentThread().name}] $msg")

fun main(args: Array<String>) {
    val ctx1 = newSingleThreadContext("Ctx1")
    val ctx2 = newSingleThreadContext("Ctx2")
    runBlocking(ctx1) {
        log("Started in ctx1")
        run(ctx2) {
            log("Working in ctx2")
        }
        log("Back to ctx1")
    }
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-context-04.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

�����2�̐V�����e�N�j�b�N�����؂��Ă��܂��B
1�͖����I�Ɏw�肳�ꂽ�R���e�L�X�g��[runBlocking]���g�p���A����1��[run]�֐����g�p���ăR���[�`���̃R���e�L�X�g��ύX���Ȃ���A�����R���[�`���ɂƂǂ܂邱�Ƃ��ȉ��̏o�͂ł킩��܂��B

```text
[Ctx1 @coroutine#1] Started in ctx1
[Ctx2 @coroutine#1] Working in ctx2
[Ctx1 @coroutine#1] Back to ctx1
```

<!--- TEST -->

### �R���e�L�X�g�ɂ�����W���u

�R���[�`����[Job]�͂��̃R���e�L�X�g�̈ꕔ�ł��B
�R���[�`���� `context[Job]` �����g���Ă��ꎩ�g�̃R���e�L�X�g������o�����Ƃ��ł��܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    println("My job is ${context[Job]}")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-context-05.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

����͎��̂悤�Ȃ��̂𐶐����܂�

```
My job is BlockingCoroutine{Active}@65ae6ba4
```

<!--- TEST lines.size == 1 && lines[0].startsWith("My job is BlockingCoroutine{Active}@") -->

[CoroutineScope]��[isActive][CoroutineScope.isActive]�� `context[Job]!!.isActive` �֗̕��ȃV���[�g�J�b�g�ł��B

### �R���[�`���̎q

�R���[�`����[context][CoroutineScope.context]���g�p���ĕʂ̃R���[�`�����N������ƁA�V�����R���[�`����[Job]�͐e�R���[�`���̃W���u�� _�q_ �ɂȂ�܂��B
�e�R���[�`�����L�����Z�������ƁA���ׂĂ̎q���ċA�I�ɃL�����Z������܂��B
  
```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    // ���炩�̃��N�G�X�g���������邽�߂ɃR���[�`�����J�n����
    val request = launch(CommonPool) {
        // ����2�̃W���u�����������B1�͕ʂ̃R���e�L�X�g
        val job1 = launch(CommonPool) {
            println("job1: I have my own context and execute independently!")
            delay(1000)
            println("job1: I am not affected by cancellation of the request")
        }
        // ��������͐e�R���e�L�X�g���p������
        val job2 = launch(context) {
            println("job2: I am a child of the request coroutine")
            delay(1000)
            println("job2: I will not execute this line if my parent request is cancelled")
        }
        // �����̃T�u�W���u�����������烊�N�G�X�g�͊���
        job1.join()
        job2.join()
    }
    delay(500)
    request.cancel() // ���N�G�X�g�̏������L�����Z��
    delay(1000) // �����N���邩�m���߂邽�߂�1�b�x�点��
    println("main: Who has survived request cancellation?")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-context-06.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̃R�[�h�̏o�͈͂ȉ��̒ʂ�ł��B

```text
job1: I have my own context and execute independently!
job2: I am a child of the request coroutine
job1: I am not affected by cancellation of the request
main: Who has survived request cancellation?
```

<!--- TEST -->

### �R���e�L�X�g�̌���

�R���[�`���̃R���e�L�X�g�́A `+` ���Z�q���g���đg�ݍ��킹�邱�Ƃ��ł��܂��B
�E���̃R���e�L�X�g�́A�����̃R���e�L�X�g�̊֘A�G���g����u�������܂��B
���Ƃ��΁A�e�R���[�`����[Job]�͌p���ł��A�f�B�X�p�b�`���͎��̂悤�ɒu���������܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    // ���炩�̃��N�G�X�g���������邽�߂ɃR���[�`�����J�n����
    val request = launch(context) { // `runBlocking` �̃R���e�L�X�g���g��
        // CommonPool��CPU�W��^�̎q�W���u�𐶐����� !!!
        val job = launch(context + CommonPool) {
            println("job: I am a child of the request coroutine, but with a different dispatcher")
            delay(1000)
            println("job: I will not execute this line if my parent request is cancelled")
        }
        job.join() // �T�u�W���u�����������烊�N�G�X�g�͊���
    }
    delay(500)
    request.cancel() // ���N�G�X�g�̏������L�����Z��
    delay(1000) // �����N���邩�m���߂邽�߂�1�b�x�点��
    println("main: Who has survived request cancellation?")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-context-07.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̃R�[�h�̗\�z����錋�ʂ͎��̂Ƃ���ł��B

```text
job: I am a child of the request coroutine, but with a different dispatcher
main: Who has survived request cancellation?
```

<!--- TEST -->

### �f�o�b�O�̂��߂̃R���[�`���̖���

�R���[�`�����p�ɂɃ��O���L�^���A�����R���[�`������̃��O���R�[�h�𑊊ւ����邾���ł悢�ꍇ�́A�����I�Ɋ��蓖�Ă�ꂽID���L���ł��B
�������A�R���[�`��������̗v���̏��������̃o�b�N�O���E���h�^�X�N�̏����ɔ����Ă���ꍇ�́A�f�o�b�O�̖ړI�Ŗ����I�ɖ��O��t��������悢�ł��傤�B
[CoroutineName]�̓X���b�h���Ɠ����@�\���ʂ����܂��B
����́A�f�o�b�O���L���ɂȂ��Ă���Ƃ��ɂ��̃R���[�`�������s���Ă���X���b�h���ɕ\������܂��B

���̗�́A���̊T�O�������Ă��܂��B

```kotlin
fun log(msg: String) = println("[${Thread.currentThread().name}] $msg")

fun main(args: Array<String>) = runBlocking(CoroutineName("main")) {
    log("Started main coroutine")
    // 2�̃o�b�N�O���E���h�l�̌v�Z�����s����
    val v1 = async(CommonPool + CoroutineName("v1coroutine")) {
        log("Computing v1")
        delay(500)
        252
    }
    val v2 = async(CommonPool + CoroutineName("v2coroutine")) {
        log("Computing v2")
        delay(1000)
        6
    }
    log("The answer for v1 / v2 = ${v1.await() / v2.await()}")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-context-08.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

`-Dkotlinx.coroutines.debug` JVM�I�v�V�����ŏo�͂���錋�ʂ͎��̂悤�ɂȂ�܂��B
 
```text
[main @main#1] Started main coroutine
[ForkJoinPool.commonPool-worker-1 @v1coroutine#2] Computing v1
[ForkJoinPool.commonPool-worker-2 @v2coroutine#3] Computing v2
[main @main#1] The answer for v1 / v2 = 42
```

<!--- TEST FLEXIBLE_THREAD -->

### �����I�ȃW���u�ɂ��L�����Z��

�R���e�L�X�g�A�q�A�W���u�Ɋւ���m�����܂Ƃ߂Ă݂܂��傤�B
�A�v���P�[�V�����Ƀ��C�t�T�C�N�������I�u�W�F�N�g������Ƃ��܂����A���̃I�u�W�F�N�g�̓R���[�`���ł͂���܂���B
���Ƃ��΁AAndroid�A�v���P�[�V�������쐬���AAndroid�A�N�e�B�r�e�B�̃R���e�L�X�g�ł��܂��܂ȃR���[�`�����N�����āA�f�[�^�̃t�F�b�`��X�V�A�A�j���[�V�����Ȃǂ̔񓯊���������s���܂��B
���������[�N������邽�߂ɃA�N�e�B�r�e�B���j�������ƁA�����̃R���[�`���͂��ׂăL�����Z������Ȃ���΂Ȃ�܂���B

�A�N�e�B�r�e�B�̃��C�t�T�C�N���Ɍ��т���[�W���u]�̃C���X�^���X���쐬���邱�ƂŁA�R���[�`���̃��C�t�T�C�N�����Ǘ����邱�Ƃ��ł��܂��B
���̗�Ɏ����悤�ɁA[Job()] [Job.invoke]�t�@�N�g���֐����g�p���ăW���u�C���X�^���X���쐬����܂��B
���ׂẴR���[�`�����R���e�L�X�g���ł��̃W���u�ŊJ�n����Ă��邱�Ƃ��m�F���Ă���A[Job.cancel]��1��Ăяo���Ƃ��ׂďI�����܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val job = Job() // ���C�t�T�C�N�����Ǘ�����W���u�I�u�W�F�N�g���쐬����
    // �f���p��10�̃R���[�`�����N�����A���ꂼ��ʂ̎��Ԃɓ��삷��
    val coroutines = List(10) { i ->
        // �����͂��ׂăW���u�I�u�W�F�N�g�̎q
        launch(context + job) { // ���C��runBlocking�X���b�h�̃R���e�L�X�g���g�p���܂����A�Ǝ��̃W���u�I�u�W�F�N�g���g�p���܂�
            delay(i * 200L) // �ς̒x�� 0ms, 200ms, 400ms, ... �Ȃ�
            println("Coroutine $i is done")
        }
    }
    println("Launched ${coroutines.size} coroutines")
    delay(500L) // 0.5�b�x������
    println("Cancelling job!")
    job.cancel() // �W���u���L�����Z��.. !!!
    delay(1000L) // �R���[�`�����܂����쒆���ǂ������m���߂邽�߂ɂ���ɒx������
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-context-09.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̗�̏o�͎͂��̒ʂ�

```text
Launched 10 coroutines
Coroutine 0 is done
Coroutine 1 is done
Coroutine 2 is done
Cancelling job!
```

<!--- TEST -->

�����̂悤�ɁA�ŏ���3�̃R���[�`�����������b�Z�[�W���o�͂��A���� `job.cancel()` ��1��̌Ăяo���ŃL�����Z������܂����B
���������āA�����������肵�Ă���Android�A�v���P�[�V�����ł́A�A�N�e�B�r�e�B���쐬���ꂽ�Ƃ��ɐe�W���u�I�u�W�F�N�g���쐬���A������q�R���[�`���Ɏg�p���A�A�N�e�B�r�e�B���j�����ꂽ�Ƃ��ɃL�����Z�����邾���ł��B

## �`���l��

�x���l�́A�R���[�`���ԂŒP��̒l��]������֗��ȕ��@��񋟂��܂��B
�`���l���́A�X�g���[���l��]��������@��񋟂��܂��B

<!--- INCLUDE .*/example-channel-([0-9]+).kt
import kotlinx.coroutines.experimental.channels.*
-->

### �`���l���̊�b

[Channel]�͊T�O�I�ɂ� `BlockingQueue` �ɔ��ɂ悭���Ă��܂��B��ȈႢ��1�́A�u���b�N���� `put` ����̑���ɃT�X�y���h[send][SendChannel.send]�A�u���b�N���� `take` ����̑���ɃT�X�y���h[receive][ReceiveChannel.receive]�������Ă��邱�Ƃł��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val channel = Channel<Int>()
    launch(CommonPool) {
        // �����CPU�g�p�ʂ������v�Z��񓯊����W�b�N��������Ȃ����A�����ł͂���5�̕����𑗂邾��
        for (x in 1..5) channel.send(x * x)
    }
    // �����Ŏ󂯎����5�̐������v�����g����
    repeat(5) { println(channel.receive()) }
    println("Done!")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-channel-01.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̃R�[�h�̏o�͈͂ȉ��̒ʂ�ł��B

```text
1
4
9
16
25
Done!
```

<!--- TEST -->

### �`���l���̃N���[�Y�Ɣ���

�L���[�Ƃ͈قȂ�A�`���l���͕��邱�Ƃɂ���Ă���ȏ�G�������g�����Ȃ����Ƃ��������Ƃ��ł��܂��B
��M���ł́A�ʏ�� `for` ���[�v���g�p���ă`���l������v�f���󂯎��ƕ֗��ł��B

�T�O�I�ɂ́A[close][SendChannel.close]�͓��ʂȃN���[�Y�g�[�N�����`���l���ɑ��M����悤�Ȃ��̂ł��B
���̃N���[�Y�g�[�N������M�����Ƃ����ɔ�������~���A�N���[�Y����O�ɈȑO�ɑ��M���ꂽ���ׂĂ̗v�f����M�����Ƃ����ۏ؂�����܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val channel = Channel<Int>()
    launch(CommonPool) {
        for (x in 1..5) channel.send(x * x)
        channel.close() // ���M����
    }
    // �����ł� `for` ���[�v���g���Ď󂯎�����l���v�����g���܂��i�`���l����������܂Łj
    for (y in channel) println(y)
    println("Done!")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-channel-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST 
1
4
9
16
25
Done!
-->

### �`���l���v���f���[�T�[�̍쐬

�R���[�`�����v�f�̃V�[�P���X�𐶐�����p�^�[���͂��Ȃ��ʓI�ł��B
����� _�v���f���[�T�[ - �R���V���[�}�[_ �p�^�[���̈ꕔ�ł���A�R���J�����g�R�[�h�ł悭�����܂��B
���̂悤�ȃv���f���[�T�[���A�p�����[�^�Ƃ���channel���Ƃ�֐��ɒ��ۉ����邱�Ƃ͂ł��܂����A���ʂ͊֐�����Ԃ��Ȃ���΂Ȃ�Ȃ��Ƃ����펯�Ƃ͋t�ɂȂ�܂��B

�v���f���[�T���ŊȒP�ɍs�����Ƃ�e�Ղɂ���[produce]�Ƃ����֗��ȃR���[�`���r���_�[�ƁA�R���V���[�}���� `for` ���[�v��u�������邱�Ƃ��ł���g���֐�[consumeEach]������܂��B

```kotlin
fun produceSquares() = produce<Int>(CommonPool) {
    for (x in 1..5) send(x * x)
}

fun main(args: Array<String>) = runBlocking<Unit> {
    val squares = produceSquares()
    squares.consumeEach { println(it) }
    println("Done!")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-channel-03.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST 
1
4
9
16
25
Done!
-->

### �p�C�v���C��

�p�C�v���C���́A1�̃R���[�`���������̒l�̃X�g���[���𐶐����Ă���p�^�[���ł��B

```kotlin
fun produceNumbers() = produce<Int>(CommonPool) {
    var x = 1
    while (true) send(x++) // 1����n�܂鐮���̖����X�g���[��
}
```

�����āA�ʂ̃R���[�`���͂��̃X�g���[��������A�������̏������s���A���̌��ʂ𐶐����Ă��܂��B
�ȉ��̗�ł́A���l�͒P�ɓ�悳��܂��B

```kotlin
fun square(numbers: ReceiveChannel<Int>) = produce<Int>(CommonPool) {
    for (x in numbers) send(x * x)
}
```

���C���R�[�h�̓p�C�v���C���S�̂��J�n���ڑ����܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val numbers = produceNumbers() // 1����̐����𐶐�����
    val squares = square(numbers) // �����𕽕��ɂ���
    for (i in 1..5) println(squares.receive()) // �ŏ���5���v�����g����
    println("Done!") // ����
    squares.cancel() // ���傫�ȃA�v���ł͂����̃R���[�`�����L�����Z������K�v������܂�
    numbers.cancel()
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-channel-04.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST 
1
4
9
16
25
Done!
-->

[�R���[�`���̓f�[�����X���b�h�Ɏ��Ă���](#�R���[�`���̓f�[�����X���b�h�Ɏ��Ă���)���߁A���̃T���v���A�v���P�[�V�����ł͂����̃R���[�`�����L�����Z������K�v�͂���܂��񂪁A���傫�ȃA�v���P�[�V�����ł̓p�C�v���C�����K�v�Ȃ��Ȃ����ꍇ�ɒ�~����K�v������܂��B
���邢�́A�p�C�v���C���R���[�`����[�R���[�`���̎q](#�R���[�`���̎q)�Ƃ��Ď��s���邱�Ƃ��ł��܂��B

### �p�C�v���C���ɂ��f��

�R���[�`���̃p�C�v���C�����g���đf���𐶐��������g���āA�p�C�v���C����O��I�Ɍ��Ă݂܂��傤�B�����̐��񂩂�n�߂܂��B����͖����I�ȃR���e�L�X�g�p�����[�^�𓱓����āA�Ăяo�������R���[�`���̎��s�𐧌�ł���悤�ɂ��܂��B
 
<!--- INCLUDE kotlinx-coroutines-core/src/test/kotlin/guide/example-channel-05.kt  
import kotlin.coroutines.experimental.CoroutineContext
-->
 
```kotlin
fun numbersFrom(context: CoroutineContext, start: Int) = produce<Int>(context) {
    var x = start
    while (true) send(x++) // infinite stream of integers from start
}
```

���̃p�C�v���C���X�e�[�W�ł́A���͐�����t�B���^�����O���āA�w�肳�ꂽ�f���Ŋ���؂�邷�ׂĂ̐��l���폜���܂��B

```kotlin
fun filter(context: CoroutineContext, numbers: ReceiveChannel<Int>, prime: Int) = produce<Int>(context) {
    for (x in numbers) if (x % prime != 0) send(x)
}
```

2����̐�����J�n���A���݂̃`���l������f�������o���A���������e�f���ɑ΂��ĐV�����p�C�v���C���X�e�[�W���J�n���邱�ƂŃp�C�v���C�����\�z���܂��B
 
```
numbersFrom(2) -> filter(2) -> filter(3) -> filter(5) -> filter(7) ... 
``` 
 
���̗�ł͍ŏ���10�̑f�����o�͂��A�p�C�v���C���S�̂����C���X���b�h�̃R���e�L�X�g�Ŏ��s���܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    var cur = numbersFrom(context, 2)
    for (i in 1..10) {
        val prime = cur.receive()
        println(prime)
        cur = filter(context, cur, prime)
    }
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-channel-05.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̃R�[�h�̏o�͂ł��B

```text
2
3
5
7
11
13
17
19
23
29
```

<!--- TEST -->

�W�����C�u������ `buildIterator` �R���[�`���r���_�[���g���ē����p�C�v���C�����\�z�ł��邱�Ƃɗ��ӂ��Ă��������B
`produce` �� `buildIterator`�A `send` �� `yield`�A `receive` �� `next`�A `ReceiveChannel` �� `Iterator` �Œu�������A�R���e�L�X�g����菜���܂��B `runBlocking` ���K�v����܂���B
�������A��L�̂悤�ȃ`���l�����g�p����p�C�v���C���̗��_�́A[CommonPool]�R���e�L�X�g�Ŏ��s����Ǝ��ۂɕ�����CPU�R�A���g�p�ł��邱�Ƃł��B

�Ƃɂ����A����͑f����������ɂ͔��ɔ���p�I�ȕ��@�ł��B ���ۂɂ̓p�C�v���C���́i�����[�g�T�[�r�X�ւ̔񓯊��Ăяo���̂悤�ȁj�������̑��̃T�X�y���h�Ăяo����K�v�Ƃ��܂��B�����̃p�C�v���C���͊��S�ɔ񓯊��� `produce` �Ƃ͈قȂ�C�ӂ̒��f�������Ȃ����߁A`buildSeqeunce` / `buildIterator` ���g�p���č\�z���邱�Ƃ͂ł��܂���B
 
### �_���o�͐�

�����̃R���[�`���������`���l�������M���A�����̊Ԃō�Ƃ𕪎U���邱�Ƃ�����܂��B
����I�ɐ����i���b10�̐��l�j�𐶐�����v���f���[�T�[�R���[�`������n�߂܂��傤�B

```kotlin
fun produceNumbers() = produce<Int>(CommonPool) {
    var x = 1 // 1����n�߂�
    while (true) {
        send(x++) // ���𐶐�
        delay(100) // 0.1�b�҂�
    }
}
```

�������̃v���Z�b�T�R���[�`���������Ƃ��ł��܂��B���̗�ł́AID�Ǝ󂯎�������l���v�����g���܂��B

```kotlin
fun launchProcessor(id: Int, channel: ReceiveChannel<Int>) = launch(CommonPool) {
    channel.consumeEach {
        println("Processor #$id received $it")
    }    
}
```

���x��5�̃v���Z�b�T���N�����āA1�b�ԓ��삳���܂��傤�B�����N���邩�m���߂Ă��������B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val producer = produceNumbers()
    repeat(5) { launchProcessor(it, producer) }
    delay(1000)
    producer.cancel() // cancel producer coroutine and thus kill them all
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-channel-06.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

�v���Z�b�TID�Ƃ��Ď󂯎�邻�ꂼ��̌ŗL�̐����͈قȂ�\��������܂����A�o�͎͂��̂悤�ɂȂ�܂��B

```
Processor #2 received 1
Processor #4 received 2
Processor #0 received 3
Processor #1 received 4
Processor #3 received 5
Processor #2 received 6
Processor #4 received 7
Processor #0 received 8
Processor #1 received 9
Processor #3 received 10
```

<!--- TEST lines.size == 10 && lines.withIndex().all { (i, line) -> line.startsWith("Processor #") && line.endsWith(" received ${i + 1}") } -->

�v���f���[�T�̃R���[�`�����L�����Z������Ƃ��̃`���l���������A�ŏI�I�Ƀv���Z�b�T�̃R���[�`�����s���Ă���`���l���ł̌J��Ԃ����I�����邱�Ƃɒ��ӂ��Ă��������B

### �_�����͐�

�����̃R���[�`���������`���l���ɑ��M���邱�Ƃ�����܂��B
���Ƃ��΁A������̃`���l���ƁA�w�肳�ꂽ��������w�肳�ꂽ�x���ł��̃`���l���ɌJ��Ԃ����M����T�X�y���h�֐��������Ă��܂��B

```kotlin
suspend fun sendString(channel: SendChannel<String>, s: String, time: Long) {
    while (true) {
        delay(time)
        channel.send(s)
    }
}
```

���āA������𑗐M����R���[�`�����������N������Ƃǂ��Ȃ邩���Ă݂܂��傤�i���̗�ł̓��C���X���b�h�̃R���e�L�X�g�ŋN�����܂��j�B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val channel = Channel<String>()
    launch(context) { sendString(channel, "foo", 200L) }
    launch(context) { sendString(channel, "BAR!", 500L) }
    repeat(6) { // receive first six
        println(channel.receive())
    }
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-channel-07.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

�o�͂́A

```text
foo
foo
BAR!
foo
foo
BAR!
```

<!--- TEST -->

### �o�b�t�@�[���ꂽ�`���l��

���܂łɎ����ꂽ�`���l���ɂ̓o�b�t�@�[������܂���ł����B �o�b�t�@�[����Ă��Ȃ��`���l���́A���M���Ǝ�M�������݂��ɏo������Ƃ��ɗv�f��]�����܂��i�ʖ������f�u�[�j�B send���ŏ��ɌĂяo���ꂽ�ꍇ�Areceive���Ăяo�����܂Œ��f����܂��Breceive���ŏ��ɌĂяo���ꂽ�ꍇ�Asend���Ăяo�����܂Œ��f����܂��B

[Channel()] [Channel.invoke]�t�@�N�g���֐���[produce]�r���_�[�́A_�o�b�t�@�[�T�C�Y_ ���w�肷�邽�߂̃I�v�V������ `capacity` �p�����[�^���Ƃ�܂��B �o�b�t�@�[�́A�w�肳�ꂽ�e�ʂ����� `BlockingQueue` �Ɠ��l�ɁA���M�������f����O�ɕ����̗v�f�𑗐M�ł���悤�ɂ��܂��B����̓o�b�t�@�[�������ς��ɂȂ�ƃu���b�N���܂��B

���̃R�[�h�̓�������Ă݂܂��傤�B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val channel = Channel<Int>(4) // �o�b�t�@�[���ꂽ�`���l�������
    launch(context) { // ���M���R���[�`�����N��
        repeat(10) {
            println("Sending $it") // �e�v�f�𑗐M����O�Ƀv�����g
            channel.send(it) // �o�b�t�@�[�������ς��ɂȂ����璆�f����
        }
    }
    // �����󂯎�炸�ɑ҂�...
    delay(1000)
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-channel-08.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

����͗e�� _4_ �̃o�b�t�@�[���ꂽ�`���l�����g���� _5_ �� "sending"��\�����܂��B

```text
Sending 0
Sending 1
Sending 2
Sending 3
Sending 4
```

<!--- TEST -->

�ŏ���4�̗v�f�̓o�b�t�@�[�ɒǉ�����A5�Ԗڂ̗v�f�𑗐M���悤�Ƃ���Ƒ��M���͒��f���܂��B


### �`���l���͌���

�`���l���ւ̑���̑��M�Ǝ�M�́A�����̃R���[�`������̌Ăяo���̏��ԂɊւ��� _����_ �ł��B 
�����̓t�@�[�X�g�C���E�t�@�[�X�g�A�E�g�̏����Œ񋟂���܂��B�Ⴆ�� `receive` ���Ăяo���ŏ��̃R���[�`���͗v�f���擾���܂��B
���̗�ł́A2�̃R���[�`��"ping"��"pong"�����L"table"�`���l������"ball"�I�u�W�F�N�g���󂯎��܂��B

```kotlin
data class Ball(var hits: Int)

fun main(args: Array<String>) = runBlocking<Unit> {
    val table = Channel<Ball>() // ���L�e�[�u��
    launch(context) { player("ping", table) }
    launch(context) { player("pong", table) }
    table.send(Ball(0)) // �{�[������������
    delay(1000) // 1�b�x�点��
    table.receive() // �Q�[���I�[�o�[�B�{�[����͂�
}

suspend fun player(name: String, table: Channel<Ball>) {
    for (ball in table) { // ���[�v�Ń{�[�����󂯎��
        ball.hits++
        println("$name $ball")
        delay(300) // �����҂�
        table.send(ball) // �{�[����߂�
    }
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-channel-09.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

"ping"�R���[�`�����ŏ��ɊJ�n�����̂ŁA�{�[�����󂯎��͍̂ŏ��̃R���[�`���ł��B "ping"�R���[�`���́A�{�[�����e�[�u���ɖ߂����シ���ɍĂу{�[�����󂯎��悤�ɂȂ��Ă��܂����A�{�[���͊��Ɏ�M��҂��Ă���"pong"�R���[�`���ɂ���Ď�M���܂��B

```text
ping Ball(hits=1)
pong Ball(hits=2)
ping Ball(hits=3)
pong Ball(hits=4)
ping Ball(hits=5)
```

<!--- TEST -->

## ���L�~���[�^�u���X�e�[�g�ƕ��s��

�R���[�`���́A[CommonPool]�̂悤�ȃ}���`�X���b�h�f�B�X�p�b�`�����g�p���ē����Ɏ��s�ł��܂��B ����́A���ׂĂ̒ʏ�̕��s���̖����N���܂��B
��Ȗ��́A**���L�~���[�^�u���X�e�[�g**�ւ̃A�N�Z�X�̓����ł��B
�R���[�`���̐��E�ł̂��̖��ɑ΂��邢�����̉�����́A�}���`�X���b�h�̐��E�̉�����Ǝ��Ă��܂����A���͓Ǝ��̂��̂ł��B

### ���

��̃R���[�`���𓯂��悤�ɐ����s���Ă݂܂��傤�i100����̎��s�j�B
����Ȃ��r�̂��߂Ɋ������Ԃ����肵�܂��B

<!--- INCLUDE .*/example-sync-([0-9]+).kt
import kotlin.coroutines.experimental.CoroutineContext
import kotlin.system.measureTimeMillis
-->

<!--- INCLUDE .*/example-sync-03.kt
import java.util.concurrent.atomic.AtomicInteger
-->

<!--- INCLUDE .*/example-sync-06.kt
import kotlinx.coroutines.experimental.sync.Mutex
-->

<!--- INCLUDE .*/example-sync-07.kt
import kotlinx.coroutines.experimental.channels.*
-->

```kotlin
suspend fun massiveRun(context: CoroutineContext, action: suspend () -> Unit) {
    val n = 1000 // �N������R���[�`���̐�
    val k = 1000 // �e�R���[�`���ɂ���ăA�N�V�������J��Ԃ�����
    val time = measureTimeMillis {
        val jobs = List(n) {
            launch(context) {
                repeat(k) { action() }
            }
        }
        jobs.forEach { it.join() }
    }
    println("Completed ${n * k} actions in $time ms")    
}
```

<!--- INCLUDE .*/example-sync-([0-9]+).kt -->

�܂��A�}���`�X���b�h�����ꂽ[CommonPool]�R���e�L�X�g���g�p���āA���L�~���[�^�u���ϐ����C���N�������g������ɒP���ȃA�N�V��������n�߂܂��B

```kotlin
var counter = 0

fun main(args: Array<String>) = runBlocking<Unit> {
    massiveRun(CommonPool) {
        counter++
    }
    println("Counter = $counter")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-sync-01.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST LINES_START
Completed 1000000 actions in
Counter =
-->

�Ō�ɉ����v�����g����܂����H ��̃R���[�`���������Ȃ��ŕ����̃X���b�h���瓯���� `counter` ���C���N�������g���邽�߁A�uCounter = 1000000�v���v�����g���邱�Ƃ͂قƂ�ǂ���܂���B

### Volatile�͏����ɂȂ�Ȃ�

�ϐ��� `volatile` �ɂ���ƕ��s���̖�肪���������Ƃ����������ʓI�ł��B ����������Ă݂܂��傤�B

```kotlin
@Volatile // Kotlin�� `volatile` �̓A�m�e�[�V����
var counter = 0

fun main(args: Array<String>) = runBlocking<Unit> {
    massiveRun(CommonPool) {
        counter++
    }
    println("Counter = $counter")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-sync-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST LINES_START
Completed 1000000 actions in
Counter =
-->

���̃R�[�h�͂��x�����삵�܂����Avolatile�ϐ��͑Ή�����ϐ��̐��`�i���p��Łu�A�g�~�b�N�v�j�ǂݏ�����ۏ؂�����̂́A���傫�ȃA�N�V�����i���̏ꍇ�̓C���N�������g�j�̃A�g�~�b�N����񋟂��Ȃ����߁A�Ō�ɁuCounter = 1000000�v�𓾂��܂���B 

### �X���b�h�Z�[�t�ȃf�[�^�\��

�X���b�h�ƃR���[�`���̗����ŋ@�\�����ʓI�ȉ�����́A���L��ԂŎ��s����K�v�����邷�ׂĂ̑���ŕK��������񋟂���X���b�h�Z�[�t�i�ʖ��A�����A���`���A�܂��̓A�g�~�b�N�j�f�[�^�\�����g�p���邱�Ƃł��B
�P���ȃJ�E���^�̏ꍇ�A�A�g�~�b�N�� `incrementAndGet` ��������� `AtomicInteger` �N���X���g�����Ƃ��ł��܂��B

```kotlin
var counter = AtomicInteger()

fun main(args: Array<String>) = runBlocking<Unit> {
    massiveRun(CommonPool) {
        counter.incrementAndGet()
    }
    println("Counter = ${counter.get()}")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-sync-03.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST ARBITRARY_TIME
Completed 1000000 actions in xxx ms
Counter = 1000000
-->

����́A���̓���̖��ɑ΂���ő��̉�����ł��B �P���ȃJ�E���^�[�A�R���N�V�����A�L���[�A���̑��̕W���I�ȃf�[�^�\���Ƃ����̊�{�I�ȑ���ł͋@�\���܂��B �������A���G�ȏ�Ԃ₷���Ɏg�p�ł���X���b�h�Z�[�t�Ȏ����������Ȃ����G�ȑ���ɂ́A�e�ՂɊg���ł��܂���B

### �ח��x�̃X���b�h�S��

_�X���b�h�S��_ �́A����̋��L��Ԃւ̂��ׂẴA�N�Z�X��1�̃X���b�h�Ɍ��肳��Ă���A���L�~���[�^�u���X�e�[�g�̖��ւ̒�Ăł��B
����͒ʏ�A���ׂĂ�UI��Ԃ��P��̃C�x���g�f�B�X�p�b�`/�A�v���P�[�V�����X���b�h�Ɍ��肳���UI�A�v���P�[�V�����Ŏg�p����܂��B �P��X���b�h�̃R���e�L�X�g���g�p���ăR���[�`���ŊȒP�ɓK�p�ł��܂��B

```kotlin
val counterContext = newSingleThreadContext("CounterContext")
var counter = 0

fun main(args: Array<String>) = runBlocking<Unit> {
    massiveRun(CommonPool) { // �e�R���[�`����CommonPool�Ŏ��s����
        run(counterContext) { // ���ꂼ��̃C���N�������g��P��X���b�h�̃R���e�L�X�g�Ɍ��肷��
            counter++
        }
    }
    println("Counter = $counter")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-sync-04.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST ARBITRARY_TIME
Completed 1000000 actions in xxx ms
Counter = 1000000
-->

���̃R�[�h�� _�ח��x_ �̃X���b�h�S�����s�����߁A���ɂ������Ɠ��삵�܂��B
�X�̃C���N�������g�� [run] �u���b�N���g�p���ă}���`�X���b�h�� `CommonPool` �R���e�L�X�g����V���O���X���b�h�̃R���e�L�X�g�ɐ؂�ւ��܂��B

### �e���x�̃X���b�h�S��

�����ɂ̓X���b�h�S���͑傫�ȃ`�����N�ōs���܂��B�Ⴆ�΁A��Ԃ��X�V����r�W�l�X���W�b�N�̑傫�ȕ����͒P��̃X���b�h�Ɍ��肳��܂��B
���̗�ł́A���̂悤�ɂ��ăV���O���X���b�h�R���e�L�X�g�Ŋe�R���[�`�����N�����Ď��s���܂��B

```kotlin
val counterContext = newSingleThreadContext("CounterContext")
var counter = 0

fun main(args: Array<String>) = runBlocking<Unit> {
    massiveRun(counterContext) { // �e�R���[�`�����V���O���X���b�h�R���e�L�X�g�Ŏ��s����
        counter++
    }
    println("Counter = $counter")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-sync-05.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST ARBITRARY_TIME
Completed 1000000 actions in xxx ms
Counter = 1000000
-->

����ŁA�͂邩�ɍ����ɓ��삵���������ʂ������܂��B

### �r������

���̖��ɑ΂���r������̉�����́A�����ē����Ɏ��s����Ȃ� _�N���e�B�J���Z�N�V����_ �ŋ��L��Ԃ̂��ׂĂ̕ύX��ی삷�邱�Ƃł��B
�u���b�N���鐢�E�ł͒ʏ� `synchronized` �܂��� `ReentrantLock` ���g�p���܂��B
�R���[�`���̑�Ă�[Mutex]�ƌĂ΂�Ă��܂��B
����̓N���e�B�J���Z�N�V��������؂�[lock][Mutex.lock]��[unlock][Mutex.unlock]�֐��������Ă��܂��B
��ȈႢ�́A `Mutex.lock` �̓T�X�y���h�֐��ł��邱�Ƃł��B
����̓X���b�h���u���b�N���܂���B

```kotlin
val mutex = Mutex()
var counter = 0

fun main(args: Array<String>) = runBlocking<Unit> {
    massiveRun(CommonPool) {
        mutex.lock()
        try { counter++ }
        finally { mutex.unlock() }
    }
    println("Counter = $counter")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-sync-06.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST ARBITRARY_TIME
Completed 1000000 actions in xxx ms
Counter = 1000000
-->

���̗�ł̃��b�N�͍ח��x�Ȃ̂ŁA�㏞�𕥂��Ă��܂��B
�������A���L��Ԃ����I�ɕύX���Ȃ���΂Ȃ�Ȃ��󋵂ɂ͓K���Ă��܂����A���̏�Ԃ����肳�ꂽ���R�ȃX���b�h�͂���܂���B

### �A�N�^�[

�A�N�^�[�́A�R���[�`���A���̃R���[�`���ɕ����߂��J�v�Z�������ꂽ��ԁA����ё��̃R���[�`���ƒʐM���邽�߂̃`���l���̑g�ݍ��킹�ł��B
�P���ȃA�N�^�[�͊֐��Ƃ��ċL�q�ł��܂����A���G�ȏ�Ԃ̃A�N�^�[�̓N���X�ɓK���Ă��܂��B

[actor]�R���[�`���r���_�[���A�N�^�[�̃��[���{�b�N�X�`���l�������b�Z�[�W����M����X�R�[�v�Ɍ������A
���ʂ̃W���u�I�u�W�F�N�g�ɑ��M�`���l������������̂ŁA�A�N�^�[�ւ̒P��̎Q�Ƃ����̃n���h���Ƃ��Ď����^�Ԃ��Ƃ��ł��܂��B

```kotlin
// counterActor�̃��b�Z�[�W�^
sealed class CounterMsg
object IncCounter : CounterMsg() // �J�E���^�[���C���N�������g���������̃��b�Z�[�W
class GetCounter(val response: SendChannel<Int>) : CounterMsg() // �ԐM�����������N�G�X�g

// ���̊֐��́A�V�����J�E���^�A�N�^���N������
fun counterActor() = actor<CounterMsg>(CommonPool) {
    var counter = 0 // �A�N�^�[�̏��
    for (msg in channel) { // ��M���b�Z�[�W�𔽕���������
        when (msg) {
            is IncCounter -> counter++
            is GetCounter -> msg.response.send(counter)
        }
    }
}

fun main(args: Array<String>) = runBlocking<Unit> {
    val counter = counterActor() // �A�N�^�[�����
    massiveRun(CommonPool) {
        counter.send(IncCounter)
    }
    val response = Channel<Int>()
    counter.send(GetCounter(response))
    println("Counter = ${response.receive()}")
    counter.close() // �A�N�^�[���I������
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-sync-07.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

<!--- TEST ARBITRARY_TIME
Completed 1000000 actions in xxx ms
Counter = 1000000
-->

�A�N�^�[���̂��ǂ̂悤�ȃR���e�L�X�g�Ŏ��s����邩�́i���m���ɂ����āj���ł͂���܂���B
�A�N�^�[�̓R���[�`���ł���R���[�`���͏��ԂɎ��s�����̂ŁA����̃R���[�`���ւ̏�Ԃ̕����߂͋��L�~���[�^�u���X�e�[�g�̖��ɑ΂��������Ƃ��ċ@�\���܂��B

���̏ꍇ�A��Ɏ��s�����Ƃ�����ʂ̃R���e�L�X�g�ɐ؂�ւ���K�v���Ȃ����߁A���ׂ̉��ł̓��b�N�����A�N�^�[�̂ق��������I�ł��B

> [actor]�R���[�`���r���_�[�͓�d��[produce]�R���[�`���r���_�[�ł��邱�Ƃɒ��ӂ��Ă��������B
  �A�N�^�[�̓��b�Z�[�W����M����`���l���Ɋ֘A�t�����A�v���f���[�T�[�͗v�f�𑗐M����`���l���Ɋ֘A�t�����܂��B

## �Z���N�g��

�Z���N�g�����g�p����ƕ����̃T�X�y���h�֐��𓯎��ɑ҂��Ƃ��ł��A���p�\�ɂȂ����ŏ��̂��̂� _�I��_ ���邱�Ƃ��ł��܂��B

<!--- INCLUDE .*/example-select-([0-9]+).kt
import kotlinx.coroutines.experimental.channels.*
import kotlinx.coroutines.experimental.selects.*
-->

### �`���l������̑I��

2�̕�����̃v���f���[�T�[�A `fizz` �� `buzz` ������܂��B `fizz` ��300�~���b���Ƃ�"Fizz"������𐶐����܂��B

<!--- INCLUDE .*/example-select-01.kt
import kotlin.coroutines.experimental.CoroutineContext
-->

```kotlin
fun fizz(context: CoroutineContext) = produce<String>(context) {
    while (true) { // 300�~���b���Ƃ� "Fizz" �𑗂�
        delay(300)
        send("Fizz")
    }
}
```

`buzz` ��500�~���b���Ƃ� "Buzz!" ������𐶐����܂��B

```kotlin
fun buzz(context: CoroutineContext) = produce<String>(context) {
    while (true) { // 500�~���b���Ƃ� "Buzz!" �𑗂�
        delay(500)
        send("Buzz!")
    }
}
```

[receive][ReceiveChannel.receive]�T�X�y���h�֐����g�p����ƁA����̃`���l������ _�܂���_ �����̃`���l�������M���邱�Ƃ��ł��܂��B
�������A[select]���́A[onReceive][SelectBuilder.onReceive]�߂��g���� _����_ ���瓯���Ɏ󂯎�邱�Ƃ��ł��܂��B

```kotlin
suspend fun selectFizzBuzz(fizz: ReceiveChannel<String>, buzz: ReceiveChannel<String>) {
    select<Unit> { // <Unit>�͂��̃Z���N�g�������ʂ𐶐����Ȃ����Ƃ��Ӗ����܂�
        fizz.onReceive { value ->  // �ŏ��̃Z���N�g��
            println("fizz -> '$value'")
        }
        buzz.onReceive { value ->  // 2�Ԗڂ̃Z���N�g��
            println("buzz -> '$value'")
        }
    }
}
```

�����S����7����s���܂��傤�B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val fizz = fizz(context)
    val buzz = buzz(context)
    repeat(7) {
        selectFizzBuzz(fizz, buzz)
    }
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-select-01.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̃R�[�h�̌��ʂ͎��̂Ƃ���ł��B

```text
fizz -> 'Fizz'
buzz -> 'Buzz!'
fizz -> 'Fizz'
fizz -> 'Fizz'
buzz -> 'Buzz!'
fizz -> 'Fizz'
buzz -> 'Buzz!'
```

<!--- TEST -->

### �N���[�Y���̑I��

�`���l���������A�Ή����� `select` ����O���X���[����ƁA `select` ��[onReceive][SelectBuilder.onReceive]�߂͎��s���܂��B
[onReceiveOrNull][SelectBuilder.onReceiveOrNull]�߂��g�p���āA�`���l��������ꂽ�Ƃ��ɓ���̃A�N�V���������s�ł��܂��B
���̗�́A `select` ���I�����ꂽ�߂̌��ʂ�Ԃ����ł��邱�Ƃ������Ă��܂��B

```kotlin
suspend fun selectAorB(a: ReceiveChannel<String>, b: ReceiveChannel<String>): String =
    select<String> {
        a.onReceiveOrNull { value -> 
            if (value == null) 
                "Channel 'a' is closed" 
            else 
                "a -> '$value'"
        }
        b.onReceiveOrNull { value -> 
            if (value == null) 
                "Channel 'b' is closed"
            else    
                "b -> '$value'"
        }
    }
```

"Hello" �������4�񐶐�����`���l�� `a` �� "World" ��4�񐶐�����`���l�� `b` ���g�p���܂��傤�B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    // ���̗�ł̓��C���X���b�h�̃R���e�L�X�g��\���\���̂��߂Ɏg�p����...
    val a = produce<String>(context) { 
        repeat(4) { send("Hello $it") }
    }
    val b = produce<String>(context) { 
        repeat(4) { send("World $it") }
    }
    repeat(8) { // �ŏ���8�̌��ʂ��v�����g����
        println(selectAorB(a, b))
    }
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-select-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̃R�[�h�̌��ʂ͔��ɋ����[���̂ŁA��������[�h�̏ڍׂŕ��͂��܂��B

```text
a -> 'Hello 0'
a -> 'Hello 1'
b -> 'World 0'
a -> 'Hello 2'
a -> 'Hello 3'
b -> 'World 1'
Channel 'a' is closed
Channel 'a' is closed
```

<!--- TEST -->

����ɂ͂������̏���������܂��B

�܂��A `select` �͍ŏ��̐߂� _�΂���_ ���܂��B
�����̐߂������ɑI���\�ȏꍇ�A�ŏ��̐߂��I������܂��B
�����ł́A�����̃`���l������ɕ�����𐶐����Ă���̂ŁA�`���l�� `a` ��select�̍ŏ��̐߂ł���A�����܂��B
�������A�o�b�t�@����Ă��Ȃ��`���l�����g�p���Ă���̂ŁA `a` ��[send][SendChannel.send]�Ăяo���Ŏ��X���f���A `b` �ɂ����M����@���^���܂��B

2�Ԗڂ̏����́A[onReceiveOrNull][SelectBuilder.onReceiveOrNull]�́A�`���l�������ɕ����Ă���Ƃ��ɒ����ɑI������邱�Ƃł��B

### ���M�̑I��

Select���ɂ́A[onSend][SelectBuilder.onSend]�߂�����A�I���̃o�C�A�X���ꂽ�����Ƒg�ݍ��킹�ĂƂĂ��L���Ɏg�p�ł��܂��B

�v���C�}���`���l���̃R���V���[�}�[�����M�ɒǂ����Ȃ��Ƃ��ɁA���̒l�� `side` �`���l���ɑ��鐮���̃v���f���[�T�[�̗�������܂��傤�B

```kotlin
fun produceNumbers(side: SendChannel<Int>) = produce<Int>(CommonPool) {
    for (num in 1..10) { // 1����10�܂ł�10�̐��𐶐�����
        delay(100) // 100�~���b����
        select<Unit> {
            onSend(num) {} // �v���C�}���`���l���ɑ���
            side.onSend(num) {} // �܂��̓T�C�h�`���l���ɑ���
        }
    }
}
```

�R���V���[�}�[�͂��Ȃ�x�����āA�e���l����������̂�250�~���b�����邱�Ƃɂ��܂��B
 
```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val side = Channel<Int>() // �T�C�h�`���l�������蓖�Ă�
    launch(context) { // ����̓T�C�h�`���l���̔��ɍ����ȃR���V���[�}�[
        side.consumeEach { println("Side channel has $it") }
    }
    produceNumbers(side).consumeEach { 
        println("Consuming $it")
        delay(250) // �}�����ɁA������l�����������������
    }
    println("Done consuming")
}
``` 
 
> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-select-03.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�
  
�ł́A�����N���邩���Ă݂܂��傤�B
 
```text
Consuming 1
Side channel has 2
Side channel has 3
Consuming 4
Side channel has 5
Side channel has 6
Consuming 7
Side channel has 8
Side channel has 9
Consuming 10
Done consuming
```

<!--- TEST -->

### �������ꂽ�l�̑I��

�x���l�́A[onAwait][SelectBuilder.onAwait]�߂��g�p���đI���ł��܂��B
�����_���x���̌�ɒx��������l��Ԃ��񓯊��֐�����n�߂܂��傤�B

<!--- INCLUDE .*/example-select-04.kt
import java.util.*
-->

```kotlin
fun asyncString(time: Int) = async(CommonPool) {
    delay(time.toLong())
    "Waited for $time ms"
}
```

�����_���Ȓx���ł����1�_�[�X�J�n���Ă݂܂��傤�B

```kotlin
fun asyncStringsList(): List<Deferred<String>> {
    val random = Random(3)
    return List(12) { asyncString(random.nextInt(1000)) }
}
```

���C���֐��͍ŏ���asyncString�֐�����������̂�҂��āA�܂��A�N�e�B�u�Ȓx���l�̐��𐔂��܂��B
`select` ����Kotlin DSL�ł��邽�߁A�C�ӂ̃R�[�h���g���Đ߂�񋟂��邱�Ƃ��ł��邱�Ƃɗ��ӂ��Ă��������B
���̏ꍇ�A�e�x���l�ɑ΂��� `onAwait` �߂�񋟂��邽�߂ɒx���l�̃��X�g�𔽕����܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val list = asyncStringsList()
    val result = select<String> {
        list.withIndex().forEach { (index, deferred) ->
            deferred.onAwait { answer ->
                "Deferred $index produced answer '$answer'"
            }
        }
    }
    println(result)
    val countActive = list.count { it.isActive }
    println("$countActive coroutines are still active")
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-select-04.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

�o�͂́A

```text
Deferred 4 produced answer 'Waited for 128 ms'
11 coroutines are still active
```

<!--- TEST -->

### �������ꂽ�l�̃`���l���̐؂�ւ�

���̒x���l�����邩�`���l����������܂ŁA�x���X�g�����O�l�̃`���l��������A��M�����x���l��҂`���l���v���f���[�T�[�֐��������܂��傤�B
���̗�ł́A���� `select` ��[onReceiveOrNull][SelectBuilder.onReceiveOrNull]�߂�[onAwait] [SelectBuilder.onAwait]�߂����Ă��܂��B

```kotlin
fun switchMapDeferreds(input: ReceiveChannel<Deferred<String>>) = produce<String>(CommonPool) {
    var current = input.receive() // �ŏ��Ɏ󂯎�����x���l����J�n����
    while (isActive) { // �L�����Z���܂��͕����Ȃ����胋�[�v����
        val next = select<Deferred<String>?> { // ����select���玟�̒x���l�܂���null��Ԃ�
            input.onReceiveOrNull { update ->
                update // �ҋ@���鎟�̒l��u��������
            }
            current.onAwait { value ->  
                send(value) // ���݂̒x�������������l�𑗐M����
                input.receiveOrNull() // ���̓`���l�����玟�̒x�����g�p����
            }
        }
        if (next == null) {
            println("Channel was closed")
            break // ���[�v���o��
        } else {
            current = next
        }
    }
}
```

������e�X�g���邽�߂ɁA�w�肵�����Ԍ�Ɏw�肳�ꂽ������ɉ��������P���Ȕ񓯊��֐����g�p���܂��B

```kotlin
fun asyncString(str: String, time: Long) = async(CommonPool) {
    delay(time)
    str
}
```

���C���֐��́A�P�� `switchMapDeferreds` �̌��ʂ��v�����g����R���[�`�����N�����A�������̃e�X�g�f�[�^�𑗐M���邾���ł��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val chan = Channel<Deferred<String>>() // �e�X�g�p�̃`���l��
    launch(context) { // �v�����g�p�̃R���[�`�����N������
        for (s in switchMapDeferreds(chan)) 
            println(s) // ��M������������v�����g����
    }
    chan.send(asyncString("BEGIN", 100))
    delay(200) // "BEGIN" �����������̂ɏ\���Ȏ���
    chan.send(asyncString("Slow", 500))
    delay(100) // slow�����������ɂ͕s�\���Ȏ���
    chan.send(asyncString("Replace", 100))
    delay(500) // �Ō�̂��̂̑O�Ɏ��Ԃ�^����
    chan.send(asyncString("END", 500))
    delay(1000) // �����Ɏ��Ԃ�^����
    chan.close() // �`���l������� ... 
    delay(500) // �I�������邽�߂ɂ��΂炭�҂�
}
```

> [����](kotlinx-coroutines-core/src/test/kotlin/guide/example-select-05.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̃R�[�h�̌��ʂ͎��̒ʂ�ł��B

```text
BEGIN
Replace
END
Channel was closed
```

<!--- TEST -->

## �Q�l����

* [Guide to UI programming with coroutines](ui/coroutines-guide-ui.md)
* [Guide to reactive streams with coroutines](reactive/coroutines-guide-reactive.md)
* [Coroutines design document (KEEP)](https://github.com/Kotlin/kotlin-coroutines/blob/master/kotlin-coroutines-informal.md)
* [Full kotlinx.coroutines API reference](http://kotlin.github.io/kotlinx.coroutines)

<!--- SITE_ROOT https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core -->
<!--- DOCS_ROOT kotlinx-coroutines-core/target/dokka/kotlinx-coroutines-core -->
<!--- INDEX kotlinx.coroutines.experimental -->
[launch]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/launch.html
[delay]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/delay.html
[runBlocking]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/run-blocking.html
[Job]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-job/index.html
[CancellationException]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-cancellation-exception.html
[yield]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/yield.html
[CoroutineScope.isActive]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-coroutine-scope/is-active.html
[CoroutineScope]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-coroutine-scope/index.html
[run]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/run.html
[NonCancellable]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-non-cancellable/index.html
[withTimeout]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/with-timeout.html
[async]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/async.html
[Deferred]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-deferred/index.html
[CoroutineStart.LAZY]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-coroutine-start/-l-a-z-y.html
[Deferred.await]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-deferred/await.html
[Job.start]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-job/start.html
[CommonPool]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-common-pool/index.html
[CoroutineDispatcher]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-coroutine-dispatcher/index.html
[CoroutineScope.context]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-coroutine-scope/context.html
[Unconfined]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-unconfined/index.html
[newCoroutineContext]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/new-coroutine-context.html
[CoroutineName]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-coroutine-name/index.html
[Job.invoke]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-job/invoke.html
[Job.cancel]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-job/cancel.html
<!--- INDEX kotlinx.coroutines.experimental.sync -->
[Mutex]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.sync/-mutex/index.html
[Mutex.lock]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.sync/-mutex/lock.html
[Mutex.unlock]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.sync/-mutex/unlock.html
<!--- INDEX kotlinx.coroutines.experimental.channels -->
[Channel]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-channel/index.html
[SendChannel.send]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-send-channel/send.html
[ReceiveChannel.receive]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-receive-channel/receive.html
[SendChannel.close]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-send-channel/close.html
[produce]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/produce.html
[consumeEach]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/consume-each.html
[Channel.invoke]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-channel/invoke.html
[actor]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/actor.html
<!--- INDEX kotlinx.coroutines.experimental.selects -->
[select]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.selects/select.html
[SelectBuilder.onReceive]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.selects/-select-builder/on-receive.html
[SelectBuilder.onReceiveOrNull]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.selects/-select-builder/on-receive-or-null.html
[SelectBuilder.onSend]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.selects/-select-builder/on-send.html
[SelectBuilder.onAwait]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.selects/-select-builder/on-await.html
<!--- END -->
