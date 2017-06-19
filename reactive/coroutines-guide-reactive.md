<!--- INCLUDE .*/example-reactive-([a-z]+)-([0-9]+)\.kt 
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

// This file was automatically generated from coroutines-guide-reactive.md by Knit tool. Do not edit.
package guide.reactive.$$1.example$$2

-->
<!--- KNIT     kotlinx-coroutines-rx2/src/test/kotlin/guide/.*\.kt -->
<!--- TEST_OUT kotlinx-coroutines-rx2/src/test/kotlin/guide/test/GuideReactiveTest.kt
// This file was automatically generated from coroutines-guide-reactive.md by Knit tool. Do not edit.
package guide.test

import org.junit.Test

class GuideReactiveTest {
-->

# �R���[�`���ɂ�郊�A�N�e�B�u�X�g���[���̃K�C�h

���̃K�C�h�ł́AKotlin�R���[�`���ƃ��A�N�e�B�u�X�g���[���̏d�v�ȈႢ�ɂ��Đ������A�������ꏏ�Ɏg�p���Ă��ǂ����ʂ𓾂���@�������܂��B
[kotlinx.coroutines�̃K�C�h](../coroutines-guide.md)�ŃJ�o�[����Ă����{�I�ȃR���[�`���̊T�O�Ɋ���Ă��Ȃ��Ă����v�ł��B ���A�N�e�B�u�X�g���[���ɐ��ʂ��Ă���ꍇ�́A���̃K�C�h���R���[�`���̐��E�ւ̂��ǂ������ɂȂ邩������܂���B

`kotlinx.coroutines` �v���W�F�N�g�ɂ́A���A�N�e�B�u�X�g���[���Ɋ֘A���邢�����̃��W���[��������܂��B

* [kotlinx-coroutines-reactive](kotlinx-coroutines-reactive) -- [���A�N�e�B�u�X�g���[��](http://www.reactive-streams.org)�̃��[�e�B���e�B
* [kotlinx-coroutines-reactor](kotlinx-coroutines-reactor) -- [Reactor](https://projectreactor.io)�̃��[�e�B���e�B
* [kotlinx-coroutines-rx1](kotlinx-coroutines-rx1) -- [RxJava 1.x](https://github.com/ReactiveX/RxJava/tree/1.x)�̃��[�e�B���e�B
* [kotlinx-coroutines-rx2](kotlinx-coroutines-rx2) -- [RxJava 2.x](https://github.com/ReactiveX/RxJava)�̃��[�e�B���e�B

���̃K�C�h�͎��[���A�N�e�B�u�X�g���[��](http://www.reactive-streams.org)�d�l�Ɋ�Â��Ă���A[RxJava 2.x](https://github.com/ReactiveX/RxJava) �Ɋ�Â��������̗�ƂƂ��� `Publisher` �C���^�[�t�F�[�X���g�p���Ă��܂��B����̓��A�N�e�B�u�X�g���[���d�l���������Ă��܂��B

�񎦂��ꂽ���ׂĂ̗�����s���邽�߂� [`kotlinx.coroutines` �v���W�F�N�g](https://github.com/Kotlin/kotlinx.coroutines)��GitHub���炠�Ȃ��̃��[�N�X�e�[�V�����ɃN���[�����邱�Ƃ����}���܂��B
�����̓v���W�F�N�g��[reactive/kotlinx-coroutines-rx2/src/test/kotlin/guide](kotlinx-coroutines-rx2/src/test/kotlin/guide)�f�B���N�g���Ɋ܂܂�Ă��܂��B
 
## �ڎ�

<!--- TOC -->

* [���A�N�e�B�u�X�g���[���ƃ`���l���̈Ⴂ](#���A�N�e�B�u�X�g���[���ƃ`���l���̈Ⴂ)
  * [�����̊�b](#�����̊�b)
  * [�T�u�X�N���v�V�����ƃL�����Z��](#�T�u�X�N���v�V�����ƃL�����Z��)
  * [�o�b�N�v���b�V���[](#�o�b�N�v���b�V���[)
  * [Rx Subject �� BroadcastChannel](#rx-subject-��-broadcastchannel)
* [���Z�q](#���Z�q)
  * [Range](#range)
  * [filter��map�̗Z��](#filter��map�̗Z��)
  * [Take until](#take-until)
  * [Merge](#merge)
* [�R���[�`���R���e�L�X�g](#�R���[�`���R���e�L�X�g)
  * [Rx�̃X���b�h](#Rx�̃X���b�h)
  * [�R���[�`���̃X���b�h](#�R���[�`���̃X���b�h)
  * [Rx observeOn](#rx-observeon)
  * [���ׂĂ𐧌䂷��R���[�`���R���e�L�X�g](#���ׂĂ𐧌䂷��R���[�`���R���e�L�X�g)
  * [Unconfined�R���e�L�X�g](#unconfined�R���e�L�X�g)

<!--- END_TOC -->

## ���A�N�e�B�u�X�g���[���ƃ`���l���̈Ⴂ

���̃Z�N�V�����ł́A���A�N�e�B�u�X�g���[���ƃR���[�`������b�Ƃ���`���l���̎�ȈႢ�̊T�v��������܂��B

### �����̊�b

[�`�����l��]�́A�ȉ��̃��A�N�e�B�u�X�g���[���N���X�Ɗ������Ă��܂��B

* ���A�N�e�B�u�X�g���[��[Publisher](https://github.com/reactive-streams/reactive-streams-jvm/blob/master/api/src/main/java/org/reactivestreams/Publisher.java)�A
* Rx Java 1.x [Observable](http://reactivex.io/RxJava/javadoc/rx/Observable.html)�A
* `Publisher` ���������� Rx Java 2.x [Flowable](http://reactivex.io/RxJava/2.x/javadoc/)�B

�����͂��ׂĖ����܂��͗L���̗v�f�iRx�Ō����A�C�e���j�̔񓯊��X�g���[�����L�q���A�����̂��ׂĂ��o�b�N�v���b�V���[���T�|�[�g���܂��B

�Ƃ���ŁA `Channel` �͏��Rx�p��Ō����Ƃ���̃A�C�e���� _�z�b�g_ �X�g���[����\���܂��B
�v�f�̓v���f���[�T�[�R���[�`���ɂ���ă`���l���ɑ��M����A�R���V���[�}�[�R���[�`���ɂ���Ď�M����܂��B
���ׂĂ�[receive][ReceiveChannel.receive]�Ăяo���́A�`���l������v�f������܂��B
���̗�ł����������܂��傤�B

<!--- INCLUDE
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.channels.*
-->

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    // 200�~���b�Ԋu�Œx������1�`3�̐��𐶐�����`�����l�����쐬����
    val source = produce<Int>(context) {
        println("Begin") // ���̃R���[�`���̊J�n���o�͂���
        for (x in 1..3) {
            delay(200) // 200�~���b�҂�
            send(x) // �`���l���ɐ��l x �𑗂�
        }
    }
    // �\�[�X����̗v�f���v�����g����
    println("Elements:")
    source.consumeEach { // �v�f�������
        println(it)
    }
    // �\�[�X����Ăїv�f���v�����g����
    println("Again:")
    source.consumeEach { // �v�f�������
        println(it)
    }
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-basic-01.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̃R�[�h�́A���̏o�͂𐶐����܂��B

```text
Elements:
Begin
1
2
3
Again:
```

<!--- TEST -->

[produce] _�R���[�`���r���_�[_ �����s�����ƁA�R���[�`����1�N�����ėv�f�̃X�g���[���𐶐����邽�߁A"Begin" �s��1�񂾂��v�����g���ꂽ���Ƃɒ��ڂ��Ă��������B
�������ꂽ�v�f�͂��ׂ�[ReceiveChannel.consumeEach][consumeEach]�g���֐��ŏ����܂��B ���̃`�����l������v�f��������x�󂯎����@�͂���܂���B
�v���f���[�T�[�̃R���[�`�����I�����A������x��M���悤�Ƃ��ĉ�����M�ł��Ȃ��ꍇ�A�`���l���͕����܂��B

`kotlinx-coroutines-core` ���W���[����[produce]�̑���� `kotlinx-coroutines-reactive` ���W���[����[publish]�R���[�`���r���_�[���g���Ă��̃R�[�h�����������܂��傤�B
�R�[�h�͓����܂܂ł����A `source` ��[ReceiveChannel]�^���g�p���Ă����Ƃ���́A���A�N�e�B�u�X�g���[����[Publisher](http://www.reactive-streams.org/reactive-streams-1.0.0-javadoc/org/reactivestreams/Publisher.html)�^�ɂȂ��Ă��܂��B

<!--- INCLUDE
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.reactive.*
-->

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    // create a publisher that produces numbers from 1 to 3 with 200ms delays between them
    val source = publish<Int>(context) {  
    //           ^^^^^^^  <---  �ȑO�̗�Ƃ̈Ⴂ�͂���
        println("Begin") // ���̃R���[�`���̊J�n���o�͂���
        for (x in 1..3) {
            delay(200) // 200�~���b�҂�
            send(x) // �`���l���ɐ��l x �𑗂�
        }
    }
    // �\�[�X����̗v�f���v�����g����
    println("Elements:")
    source.consumeEach { // �v�f�������
        println(it)
    }
    // �\�[�X����Ăїv�f���v�����g����
    println("Again:")
    source.consumeEach { // �v�f�������
        println(it)
    }
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-basic-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���x�͂��̃R�[�h�̏o�͂����̂悤�ɕς��܂��B

```text
Elements:
Begin
1
2
3
Again:
Begin
1
2
3
```

<!--- TEST -->

���̗�ł́A���A�N�e�B�u�X�g���[���ƃ`���l���̎�ȈႢ���������Ă��܂��B���A�N�e�B�u�X�g���[���͍����̋@�\�̊T�O�ł��B
�`���l���͗v�f�̃X�g���[���ł����A���A�N�e�B�u�X�g���[���͗v�f�̃X�g���[���̐������@�Ɋւ��郌�V�s���`���܂��B
_�T�u�X�N���v�V����_ �̗v�f�̎��ۂ̃X�g���[���ɂȂ�܂��B
�e�T�u�X�N���C�o�́A `Publisher` �̑Ή�����������ǂ̂悤�ɋ@�\���邩�ɉ����āA�����܂��͈قȂ�v�f�̃X�g���[�����󂯎�邱�Ƃ��ł��܂��B

��L�̗�Ŏg�p����Ă���[publich]�R���[�`���r���_�[�́A�e�T�u�X�N���v�V�����ŐV�����R���[�`�����N�����܂��B
���ׂĂ�[Publisher.consumeEach][org.reactivestreams.Publisher.consumeEach]�Ăяo���́A�V�N�ȃT�u�X�N���v�V�������쐬���܂��B
���̃R�[�h�ɂ�2����܂��B���̂��߁A"Begin" ��2��v�����g����Ă��邱�Ƃ��킩��܂��B

Rx�p��ł́A����� _�R�[���h_ �p�u���b�V���[�ƌĂ΂�܂��B�����̕W��Rx���Z�q���R�[���h�X�g���[���𐶐����܂��B
�R���[�`�����炻���𔽕����邱�Ƃ��ł��A���ׂẴT�u�X�N���v�V�����͓����v�f�̃X�g���[���𐶐����܂��B

> Rx [publish](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html#publish())���Z�q��[connect](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/flowables/ConnectableFlowable.html#connect())���\�b�h���g���āA�`�����l���Ō����̂Ɠ����U�镑�����Č��ł��܂��B

### �T�u�X�N���v�V�����ƃL�����Z��

�O�̃Z�N�V�����̗�ł́A `source.consumeEach { ... }` �X�j�y�b�g���g�p���ăT�u�X�N���v�V�������J���A�������炷�ׂĂ̗v�f���󂯎���Ă��܂��B
�`�����l������󂯎���Ă���v�f���ǂ��������邩�������ƃR���g���[������K�v������ꍇ�́A���̗�̂悤��[Publisher.open][org.reactivestreams.Publisher.open]���g�p�ł��܂��B

<!--- INCLUDE
import io.reactivex.*
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.reactive.*
-->

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val source = Flowable.range(1, 5) // 5�̐��l�̃����W
        .doOnSubscribe { println("OnSubscribe") } // ���@��񋟂���
        .doFinally { println("Finally") }         // ... �����N���Ă��邩
    var cnt = 0 
    source.open().use { channel -> // �\�[�X�̃`���l�����J��
        for (x in channel) { // �������ă`���l������v�f���󂯎��
            println(x)
            if (++cnt >= 3) break // 3�̗v�f���v�����g�����璆�~����
        }
        // ���̃R�[�h�u���b�N����������ƁA `use` ���`���l�������
    }
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-basic-03.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̏o�͂���������܂��B

```text
OnSubscribe
1
2
3
Finally
```

<!--- TEST -->
 
�����I�� `open` ���w�肷��ƁA�Ή�����T�u�X�N���v�V������[close][SubscriptionReceiveChannel.close]���āA�\�[�X����̓o�^����������K�v������܂��B
�������A�����I�� `close` ���Ăяo�̂ł͂Ȃ��A���̃R�[�h��Kotlin�̕W�����C�u������[use](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/use.html)�֐��ɗ����Ă��܂��B
�C���X�g�[�����ꂽ[doFinally](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html#doFinally(io.reactivex.functions.Action))���X�i�[�́A�T�u�X�N���v�V���������ۂɕ����Ă��邱�Ƃ��m�F���邽�߂� "Finally" ��\�����܂��B

�p�u���b�V���[���o�͂������ׂẴA�C�e���ɑ΂��Ĕ������������s����ꍇ�A`consumeEach` �ɂ���Ď����I�ɕ����Ă���̂Ŗ����I�� `close` ���g���K�v�͂���܂���B

<!--- INCLUDE
import io.reactivex.*
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.reactive.*
-->

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val source = Flowable.range(1, 5) // 5�̐��l�̃����W
        .doOnSubscribe { println("OnSubscribe") } // ���@��񋟂���
        .doFinally { println("Finally") }         // ... �����N���Ă��邩
    // �\�[�X�����ׂĔ�������
    source.consumeEach { println(it) }
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-basic-04.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̏o�͂������܂��B

```text
OnSubscribe
1
2
3
4
Finally
5
```

<!--- TEST -->

�Ō�̗v�f "5" �̑O�� "Finally" ���ǂ̂悤�ɏo�͂���邩�ɒ��ӂ��Ă��������B
����́A���̗�� `main` �֐���[runBlocking]�R���[�`���r���_�[�Ŏn�܂�R���[�`���ł��邽�߂ɋN����܂��B
���C���R���[�`���� `source.consumeEach { ... }` �����g���ă`���l���Ŏ�M���܂��B
���C���R���[�`���́A�\�[�X���A�C�e�����o�͂���̂�҂� _���f_ ����܂��B
�Ō�̃A�C�e���� `Flowable.range(1�A5)` �ɂ���ďo�͂����ƃ��C���R���[�`���� _�ĊJ_ ����A���C���X���b�h�Ƀf�B�X�p�b�`����čŌ�̗v�f����Ńv�����g���܂��B�\�[�X�͊������A"Finally" ���v�����g���܂��B

### �o�b�N�v���b�V���[

�o�b�N�v���b�V���[�́A���A�N�e�B�u�X�g���[���̒��ōł������[�����G�ȓ�����1�ł��B
�R���[�`���� _���f_ ���邱�Ƃ��ł��A�o�b�N�v���b�V���[���������邽�߂̎��R�ȓ�����񋟂��܂��B

Rx Java 2.x�ł́A�o�b�N�v���b�V���[�Ή��N���X��[Flowable](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html)�ƌĂ΂�܂��B
���̗�ł́A `kotlinx-coroutines-rx2` ���W���[����[rxFlowable]�R���[�`���r���_�[���g�p���āA1����3�܂ł�3�̐����𑗐M����flowable���`���܂��B
[send][SendChannel.send]�T�X�y���h�֐����Ăяo���O�ɏo�͂Ƀ��b�Z�[�W���v�����g���A���̑�����@�𒲂ׂ邱�Ƃ��ł��܂��B

�����̓��C���X���b�h�̃R���e�L�X�g�Ő�������܂����A�T�u�X�N���v�V�����̓T�C�Y1�̃o�b�t�@��Rx [observeOn](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html#observeOn(io.reactivex.Scheduler,%20boolean,%20int))���Z�q���g�p���ĕʂ̃X���b�h�Ɉڂ���܂��B
�T�u�X�N���C�o�[�͒x���ł��B `Thread.sleep` ���g���ăV�~�����[�g����e�A�C�e������������̂�500�~���b������܂��B

<!--- INCLUDE
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.rx2.rxFlowable
import io.reactivex.schedulers.Schedulers
-->

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> { 
    // �R���[�`�� - ���C���X���b�h�R���e�L�X�g�ɂ�����v�f�̍����v���f���[�T�[
    val source = rxFlowable(context) {
        for (x in 1..3) {
            send(x) // ����̓T�X�y���h�֐�
            println("Sent $x") // �A�C�e��������ɑ��M���ꂽ��Ƀv�����g����
        }
    }
    // Rx���g���ĕʂ̃X���b�h�̒ᑬ�̃T�u�X�N���C�o�[�ōw�ǂ���
    source
        .observeOn(Schedulers.io(), false, 1) // 1�A�C�e�����̃o�b�t�@�[�T�C�Y���w��
        .doOnComplete { println("Complete") }
        .subscribe { x ->
            Thread.sleep(500) // �e�A�C�e������������̂�500�~���b
            println("Processed $x")
        }
    delay(2000) // ���b�ԃ��C���X���b�h�𒆒f
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-basic-05.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̃R�[�h�̏o�͂́A�R���[�`���Ńo�b�N�v���b�V�����ǂ̂悤�ɋ@�\���邩�����܂������Ă��܂��B

```text
Sent 1
Processed 1
Sent 2
Processed 2
Sent 3
Processed 3
Complete
```

<!--- TEST -->

�����ł́A�v���f���[�T�[�̃R���[�`�����ŏ��̗v�f���o�b�t�@�ɓ���A�ʂ̗v�f�𑗐M���悤�Ƃ��Ă���Ԓ��f����Ă��邱�Ƃ��킩��܂��B
�R���V���[�}�[���ŏ��̃A�C�e��������������ł̂݁A�v���f���[�T�[��2�Ԗڂ̃A�C�e���𑗐M���čĊJ���܂��B

### Rx Subject �� BroadcastChannel

RxJava�ɂ́A���ׂẴT�u�X�N���C�o�[�ɗv�f�����ʓI�Ƀu���[�h�L���X�g����I�u�W�F�N�g�ł���[Subject](https://github.com/ReactiveX/RxJava/wiki/Subject)�Ƃ����T�O������܂��B
�R���[�`���̐��E�ň�v����T�O��[BroadcastChannel]�ƌĂ΂�܂��B
Rx�ɂ́A[BehaviorSubject](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/subjects/BehaviorSubject.html)����Ԃ��Ǘ����邽�߂Ɏg�p�������̂ł���悤�ɁA�l�X�ȃT�u�W�F�N�g������܂��B

<!--- INCLUDE
import io.reactivex.subjects.BehaviorSubject
-->

```kotlin
fun main(args: Array<String>) {
    val subject = BehaviorSubject.create<String>()
    subject.onNext("one")
    subject.onNext("two") // BehaviorSubject�̏�Ԃ��X�V���A"1"�̒l��������
    // �����ł��̃T�u�W�F�N�g���w�ǂ��Ă��ׂĂ��v�����g����
    subject.subscribe(System.out::println)
    subject.onNext("three")
    subject.onNext("four")
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-basic-06.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̃R�[�h�́A�T�u�X�N���v�V�����Ƃ��̂��ׂĂ̍X�Ȃ�A�b�v�f�[�g�ŃT�u�W�F�N�g�̌��݂̏�Ԃ��v�����g���܂��B

```text
two
three
four
```

<!--- TEST -->

���̃��A�N�e�B�u�X�g���[���Ɠ��l�ɁA�R���[�`������T�u�W�F�N�g���w�ǂ��邱�Ƃ��ł��܂��B
   
<!--- INCLUDE 
import io.reactivex.subjects.BehaviorSubject
import kotlinx.coroutines.experimental.Unconfined
import kotlinx.coroutines.experimental.launch
import kotlinx.coroutines.experimental.runBlocking
import kotlinx.coroutines.experimental.rx2.consumeEach
-->   
   
```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val subject = BehaviorSubject.create<String>()
    subject.onNext("one")
    subject.onNext("two")
    // ���ׂĂ��������R���[�`�����N������
    launch(Unconfined) { // �����̂Ȃ��R���e�L�X�g�ŃR���[�`�����N������
        subject.consumeEach { println(it) }
    }
    subject.onNext("three")
    subject.onNext("four")
}
```   

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-basic-07.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���ʂ͓����ł��B

```text
two
three
four
```

<!--- TEST -->

�����ł́A[Unconfined]�R���[�`���R���e�L�X�g���g�p���āARx�̃T�u�X�N���v�V�����Ɠ���������������R���[�`�����N�����܂��B
��{�I�ɂ́A�N�������R���[�`���͗v�f���o�͂����̂Ɠ����X���b�h�Œ����Ɏ��s����邱�Ƃ��Ӗ����܂��B
�R���e�L�X�g�̏ڍׂɂ��ẮA[�ʂ̃Z�N�V����](#�R���[�`���R���e�L�X�g)���Q�Ƃ��Ă��������B

�R���[�`���̗��_�́A�V���O���X���b�h��UI�X�V�̏W�񓮍���ȒP�ɓ����邱�Ƃł��B
�T�^�I��UI�A�v���P�[�V�����́A���ׂĂ̏�ԕύX�ɔ�������K�v�͂���܂���B�ŐV�̏�Ԃ݂̂��֌W���܂��B
UI�X���b�h����������Ƃ����ɁA�A�v���P�[�V�����̏�Ԃɑ΂����A�̘A�������X�V��1�x����UI�ɔ��f������K�v������܂��B
���̗�ł́A���C���X���b�h�̃R���e�L�X�g�ŏ���R���[�`�����N�����A[yield]�֐����g�p���Ĉ�A�̍X�V�̒��f���V�~�����[�g�����C���X���b�h��������邱�ƂŁA������V�~�����[�g���܂��B

<!--- INCLUDE
import io.reactivex.subjects.BehaviorSubject
import kotlinx.coroutines.experimental.launch
import kotlinx.coroutines.experimental.runBlocking
import kotlinx.coroutines.experimental.rx2.consumeEach
import kotlinx.coroutines.experimental.yield
-->

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val subject = BehaviorSubject.create<String>()
    subject.onNext("one")
    subject.onNext("two")
    // �ŐV�̍X�V���v�����g����R���[�`�����N��
    launch(context) { // �R���[�`���̃��C���X���b�h�̃R���e�L�X�g���g�p����
        subject.consumeEach { println(it) }
    }
    subject.onNext("three")
    subject.onNext("four")
    yield() // �N�������R���[�`���փ��C���X���b�h������ <--- ����
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-basic-08.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

�R���[�`���͍ŐV�̃A�b�v�f�[�g�݂̂������i�v�����g�j���܂��B

```text
four
```

<!--- TEST -->

�����ȃR���[�`���̐��E�ł���ɑ������鋓���́A[ConflatedBroadcastChannel]�ɂ���Ď�������Ă��܂��B����̓u���b�W���o�R���ă��A�N�e�B�u�X�g���[���ɍs�����ƂȂ��A�R���[�`���`���l���̏�ɓ������W�b�N�𒼐ڒ񋟂��܂��B

<!--- INCLUDE
import kotlinx.coroutines.experimental.channels.ConflatedBroadcastChannel
import kotlinx.coroutines.experimental.channels.consumeEach
import kotlinx.coroutines.experimental.launch
import kotlinx.coroutines.experimental.runBlocking
import kotlinx.coroutines.experimental.yield
-->

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val broadcast = ConflatedBroadcastChannel<String>()
    broadcast.offer("one")
    broadcast.offer("two")
    // �ŐV�̍X�V���v�����g����R���[�`�����N��
    launch(context) { // �R���[�`���̃��C���X���b�h�̃R���e�L�X�g���g�p����
        broadcast.consumeEach { println(it) }
    }
    broadcast.offer("three")
    broadcast.offer("four")
    yield() // �N�������R���[�`���փ��C���X���b�h������
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-basic-09.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

`BehaviorSubject` �Ɋ�Â��O�̗�Ɠ����o�͂𐶐����܂��B

```text
four
```

<!--- TEST -->

[BroadcastChannel]�̕ʂ̎�����[ArrayBroadcastChannel]�ł��B
�Ή�����T�u�X�N���v�V�������J����Ă���e�T�u�X�N���C�o�ɂ��ׂẴC�x���g��z�M���܂��B
Rx��[PublishSubject](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/subjects/PublishSubject.html)�ɑ������܂��B
`ArrayBroadcastChannel` �̃R���X�g���N�^���̃o�b�t�@�̗e�ʂ́A��M�����v�f���󂯎��̂𑗐M�����҂����ɑ��M�ł���v�f�̐��𐧌䂵�܂��B

## ���Z�q

Rx�̂悤�ȃt���@�\�̃��A�N�e�B�u�X�g���[�����C�u�����ɂ́A�X�g���[�����쐬�A�ϊ��A�����A����т��̑��̕��@�ŏ������邽�߂�[���ɑ����̉��Z�q](http://reactivex.io/documentation/operators.html)���t�����Ă��܂��B �o�b�N�v���b�V���[���T�|�[�g����Ǝ��̉��Z�q���쐬���邱�Ƃ�[���](https://github.com/ReactiveX/RxJava/wiki/Writing-operators-for-2.0)���Ƃ�[�L��](http://akarnokd.blogspot.ru/2015/05/pitfalls-of-operator-implementations.html)�ł��B

�R���[�`���ƃ`�����l���͋t�̌o����񋟂���悤�ɐ݌v����Ă��܂��B
�g�ݍ��݂̉��Z�q�͂���܂��񂪁A�G�������g�̃X�g���[������������͔̂��ɊȒP�ŁA�o�b�N�v���b�V���[�͖����I�ɍl����K�v�Ȃ������I�ɃT�|�[�g����܂��B

���̃Z�N�V�����ł́A�������̃��A�N�e�B�u�X�g���[�����Z�q�̃R���[�`���x�[�X�̎����������܂��B

### Range

���A�N�e�B�u�X�g���[���� `Publisher` �C���^�[�t�F�[�X�̂��߂ɁA[range](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html#range(int,%20int))���Z�q�̓Ǝ��̎�����W�J���܂��傤�B
���A�N�e�B�u�X�g���[���p�̂��̉��Z�q�̔񓯊��̂��ꂢ�Ȏ����ɂ��ẮA[���̃u���O�L��](http://akarnokd.blogspot.ru/2017/03/java-9-flow-api-asynchronous-integer.html)�Ő������Ă��܂��B
����͑����̃R�[�h��K�v�Ƃ��܂��B
�R���[�`�����g�����R�[�h���ȉ��Ɏ����܂��B

<!--- INCLUDE
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.reactive.*
import kotlin.coroutines.experimental.CoroutineContext
-->

```kotlin
fun range(context: CoroutineContext, start: Int, count: Int) = publish<Int>(context) {
    for (x in start until start + count) send(x)
}
```

���̃R�[�h�ł́A `Executor` �̑���� `CoroutineContext` ���g�p����Ă��܂��B�܂��A�o�b�N�v���b�V���[�̂��ׂĂ̑��ʂ̓R���[�`���̎d�g�݂ň����܂��B
���̎����́A `Publisher` �C���^�[�t�F�C�X�Ƃ��̒��Ԃ��`���鏬���ȃ��A�N�e�B�u�X�g���[�����C�u�����݂̂Ɉˑ����Ă��邱�Ƃɒ��ӂ��Ă��������B

�R���[�`������g�p����̂͊ȒP�ł��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    range(CommonPool, 1, 5).consumeEach { println(it) }
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-operators-01.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���̃R�[�h�̌��ʂ͋ɂ߂ē��R�ł��B
   
```text
1
2
3
4
5
```

<!--- TEST -->

### [filter��map�̗Z��

[filter](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html#filter(io.reactivex.functions.Predicate))��[map](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html#map(io.reactivex.functions.Function))�̂悤�ȃ��A�N�e�B�u���Z�q�́A�R���[�`���Ŏ�������̂͊ȒP�ł��B
������Ƃ����`�������W�ƃV���[�P�[�X�̂��߂ɁA������P��� `fusedFilterMap` ���Z�q�ɑg�ݍ��킹�܂��傤�B

<!--- INCLUDE
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.reactive.*
import org.reactivestreams.Publisher
import kotlin.coroutines.experimental.CoroutineContext
-->

```kotlin
fun <T, R> Publisher<T>.fusedFilterMap(
    context: CoroutineContext,   // ���̃R���[�`�������s���邽�߂̃R���e�L�X�g
    predicate: (T) -> Boolean,   // �t�B���^�[�q��
    mapper: (T) -> R             // mapper�֐�
) = publish<R>(context) {
    consumeEach {                // �\�[�X�X�g���[���������
        if (predicate(it))       // �t�B���^�[��
            send(mapper(it))     // �}�b�v��
    }        
}
```

�O�̗�� `range` ���g���ƁA�����Ƀt�B���^�����O���ĕ�����Ƀ}�b�s���O���� `fusedFilterMap` �̃e�X�g���ł��܂��B

<!--- INCLUDE

fun range(context: CoroutineContext, start: Int, count: Int) = publish<Int>(context) {
    for (x in start until start + count) send(x)
}
-->

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
   range(context, 1, 5)
       .fusedFilterMap(context, { it % 2 == 0}, { "$it is even" })
       .consumeEach { println(it) } // ���ʂ̕���������ׂăv�����g����
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-operators-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���ʂ��m�F����͓̂���Ȃ��A���̂悤�ɂȂ�ł��傤�B

```text
2 is even
4 is even
```

<!--- TEST -->

### Take until

�Ǝ��̃o�[�W������[takeUntil](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html#takeUntil(org.reactivestreams.Publisher))���Z�q���������܂��傤�B
2�̃X�g���[���ւ̃T�u�X�N���v�V������ǐՂ��ĊǗ�����K�v�����邽�߁A��������͔̂���[���](http://akarnokd.blogspot.ru/2015/05/pitfalls-of-operator-implementations.html)���̂ł��B
���̃X�g���[�����������邩�����𑗏o����܂ŁA�\�[�X�X�g���[�����炷�ׂĂ̗v�f�������[����K�v������܂��B
�������A�R���[�`���̎�����������[select]��������܂��B

<!--- INCLUDE
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.reactive.*
import org.reactivestreams.Publisher
import kotlin.coroutines.experimental.CoroutineContext
import kotlinx.coroutines.experimental.selects.whileSelect
-->

```kotlin
fun <T, U> Publisher<T>.takeUntil(context: CoroutineContext, other: Publisher<U>) = publish<T>(context) {
    this@takeUntil.open().use { thisChannel ->           // Publisher<T>�̃`���l���𖾎��I�ɊJ��
        other.open().use { otherChannel ->               // Publisher<U>�̃`���l���𖾎��I�ɊJ��
            whileSelect {
                otherChannel.onReceive { false }         // `other` ���牽���v�f���󂯎������E�o����
                thisChannel.onReceive { send(it); true } // thisChannel�̗v�f���đ����đ��s����
            }
        }
    }
}
```

���̃R�[�h�́A `while(select{...}) {}` ���[�v�̂��ǂ��V���[�g�J�b�g�Ƃ���[whileSelect]���g�p���AKotlin��[use]���ɂ���ďI�����Ƀ`���l������A�Ή�����p�u���b�V���[�̍w�ǂ��������܂��B

�ȉ��̌��ߑł���[range](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html#range(int,%20int))��[interval](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html#interval(long,%20java.util.concurrent.TimeUnit,%20io.reactivex.Scheduler))�̑g�ݍ��킹���e�X�g�Ɏg�p����܂��B
`publish` �R���[�`���r���_�[���g�p���ăR�[�h������Ă��܂��i������Rx�̎����͌�̃Z�N�V�����Ő������Ă��܂��j�B

```kotlin
fun rangeWithInterval(context: CoroutineContext, time: Long, start: Int, count: Int) = publish<Int>(context) {
    for (x in start until start + count) { 
        delay(time) // �e���l�𑗂�O�ɑ҂�
        send(x)
    }
}
```

���̃R�[�h�� `takeUntil` �̓����������Ă��܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    val slowNums = rangeWithInterval(context, 200, 1, 10)         // 200�~���b�Ԋu�̐���
    val stop = rangeWithInterval(context, 500, 1, 10)             // �ŏ��̂��̂�500�~���b��
    slowNums.takeUntil(context, stop).consumeEach { println(it) } // �e�X�g���Ă݂�
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-operators-03.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

�o�͂́A

```text
1
2
```

<!--- TEST -->

### Merge

�R���[�`���ŕ����̃f�[�^�X�g���[������������ɂ́A��ɏ��Ȃ��Ƃ�2�̕��@������܂��B
�O�̗�ł́A[select]�𔺂�1�̕��@��������Ă��܂����B
����1�̕��@�́A�����̃R���[�`�����N�����邱�Ƃł��B ��҂̎�@���g����[merge](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html#merge(org.reactivestreams.Publisher))���Z�q���������܂��傤�B

<!--- INCLUDE
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.reactive.*
import org.reactivestreams.Publisher
import kotlin.coroutines.experimental.CoroutineContext
-->

```kotlin
fun <T> Publisher<Publisher<T>>.merge(context: CoroutineContext) = publish<T>(context) {
  consumeEach { pub ->                 // �\�[�X�`�����l�������M�����e�p�u���b�V���[
      launch(this.context) {           // �q�R���[�`�����N��
          pub.consumeEach { send(it) } // ���̃p�u���b�V���[���炷�ׂĂ̗v�f���đ�����
      }
  }
}
```

��: [launch]�R���[�`���r���_�[�̌Ăяo���� `this.context` ���g�p���܂��B [publish]�r���_�[�ɂ���Ē񋟂����[CoroutineScope.context]���Q�Ƃ��邽�߂Ɏg�p����܂��B
���̂悤�ɂ��āA�����ŊJ�n���ꂽ�R���[�`���� `publish` �R���[�`����[children](../coroutines-guide.md#children-of-a-coroutine)�ł���A`publish` �R���[�`�����L�����Z�����ꂽ�ꍇ�⊮�������ꍇ�ɃL�����Z������܂��B
���̎����́A���̃p�u���b�V���[����������Ƃ����Ɋ������܂��B

�e�X�g�̂��߂ɁA�O�̗�� `rangeWithInterval` �֐��ƁA�����炩�x��Ă��̌��ʂ�2�񑗂�v���f���[�T�[���������Ƃ���n�߂܂��傤�B

<!--- INCLUDE

fun rangeWithInterval(context: CoroutineContext, time: Long, start: Int, count: Int) = publish<Int>(context) {
    for (x in start until start + count) { 
        delay(time) // �e���l�𑗐M����O�ɑ҂�
        send(x)
    }
}
-->

```kotlin
fun testPub(context: CoroutineContext) = publish<Publisher<Int>>(context) {
    send(rangeWithInterval(context, 250, 1, 4)) // ���l 1 �� 250ms, 2 �� 500ms, 3 �� 750ms, 4 �� 1000ms 
    delay(100) // 100ms�҂�
    send(rangeWithInterval(context, 500, 11, 3)) // ���l 11 �� 600ms, 12 �� 1100ms, 13 �� 1600ms
    delay(1100) // 1.1�b�҂� - �J�n����1.2�b��Ɋ���
}
```

���̃e�X�g�R�[�h�́A `testPub` �� `merge` ���g���A���ʂ�\�����܂��B

```kotlin
fun main(args: Array<String>) = runBlocking<Unit> {
    testPub(context).merge(context).consumeEach { println(it) } // �X�g���[���S�̂��v�����g����
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-operators-04.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���ʂ͎��̂悤�ɂȂ�܂��B

```text
1
2
11
3
4
12
```

<!--- TEST -->

## �R���[�`���R���e�L�X�g

�O�̃Z�N�V�����Ŏ��������ׂẲ��Z�q�̗�ɂ͖����I��[CoroutineContext](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.coroutines.experimental/-coroutine-context/)�p�����[�^������܂��B
Rx�̐��E�ł́A����͂����悻[Scheduler](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Scheduler.html)�ɑ������܂��B

### Rx�̃X���b�h

���̗�́ARx�ł̃X���b�h�R���e�L�X�g�Ǘ��̊�{�������Ă��܂��B
������ `rangeWithIntervalRx` ��Rx `zip`�A `range` �A `interval` ���Z�q���g���� `rangeWithInterval` �֐��̎����ł��B

<!--- INCLUDE
import io.reactivex.*
import io.reactivex.functions.BiFunction
import io.reactivex.schedulers.Schedulers
import java.util.concurrent.TimeUnit
-->

```kotlin
fun rangeWithIntervalRx(scheduler: Scheduler, time: Long, start: Int, count: Int): Flowable<Int> = 
    Flowable.zip(
        Flowable.range(start, count),
        Flowable.interval(time, TimeUnit.MILLISECONDS, scheduler),
        BiFunction { x, _ -> x })

fun main(args: Array<String>) {
    rangeWithIntervalRx(Schedulers.computation(), 100, 1, 3)
        .subscribe { println("$it on thread ${Thread.currentThread().name}") }
    Thread.sleep(1000)
}
```

> [����]�Ŋ��S�ȃR�[�h���擾�ł��܂�(kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-context-01.kt)

`rangeWithIntervalRx` ���Z�q�ɖ����I��[Schedulers.computation()](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/schedulers/Schedulers.html#computation())�X�P�W���[���[��n���Ă��܂��B�����Rx�v�Z�X���b�h�v�[���Ŏ��s����܂��B
�o�͎͂��̂悤�ɂȂ�܂��B

```text
1 on thread RxComputationThreadPool-1
2 on thread RxComputationThreadPool-1
3 on thread RxComputationThreadPool-1
```

<!--- TEST FLEXIBLE_THREAD -->

### �R���[�`���̃X���b�h

�R���[�`���̐��E�ł́A `Schedulers.computation()` ��[CommonPool]�ɂقڑΉ����Ă���̂ŁA�O�̗�͎��̗�Ɏ��Ă��܂��B

<!--- INCLUDE
import io.reactivex.*
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.reactive.*
import kotlin.coroutines.experimental.CoroutineContext
-->

```kotlin
fun rangeWithInterval(context: CoroutineContext, time: Long, start: Int, count: Int) = publish<Int>(context) {
    for (x in start until start + count) { 
        delay(time) // �e���l�𑗐M����O�ɑ҂�
        send(x)
    }
}

fun main(args: Array<String>) {
    Flowable.fromPublisher(rangeWithInterval(CommonPool, 100, 1, 3))
        .subscribe { println("$it on thread ${Thread.currentThread().name}") }
    Thread.sleep(1000)
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-context-02.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���������o�͎͂��̂悤�ɂȂ�܂��B

```text
1 on thread ForkJoinPool.commonPool-worker-1
2 on thread ForkJoinPool.commonPool-worker-1
3 on thread ForkJoinPool.commonPool-worker-1
```

<!--- TEST LINES_START -->

�����ł́A�Ǝ��̃X�P�W���[���[���������A�p�u���b�V���[�Ɠ����X���b�h�œ��삷��Rx [subscribe](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html#subscribe(io.reactivex.functions.Consumer))���Z�q���g�p���܂����B���̗�ł� `CommonPool` ���g�p���Ă��܂��B

### Rx observeOn

Rx�ł͓��ʂȉ��Z�q���g�p���ă`�F�[�����̑���̃X���b�h�R���e�L�X�g��ύX���܂��B
�܂�����Ă��Ȃ��ꍇ�A�����ɂ��Ă�[�ǂ��K�C�h](http://tomstechnicalblog.blogspot.ru/2016/02/rxjava-understanding-observeon-and.html)�������邱�Ƃ��ł��܂��B

���Ƃ��΁A[observeOn](http://reactivex.io/RxJava/2.x/javadoc/io/reactivex/Flowable.html#observeOn(io.reactivex.Scheduler))���Z�q������܂��B
`Schedulers.computation()` ���g���ăI�u�U�[�u���邽�߂ɑO�̗���C�����܂��傤�B

<!--- INCLUDE
import io.reactivex.*
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.reactive.*
import io.reactivex.schedulers.Schedulers
import kotlin.coroutines.experimental.CoroutineContext
-->

```kotlin
fun rangeWithInterval(context: CoroutineContext, time: Long, start: Int, count: Int) = publish<Int>(context) {
    for (x in start until start + count) { 
        delay(time) // �e���l�𑗐M����O�ɑ҂�
        send(x)
    }
}

fun main(args: Array<String>) {
    Flowable.fromPublisher(rangeWithInterval(CommonPool, 100, 1, 3))
        .observeOn(Schedulers.computation())                           // <-- ���̍s���ǉ����ꂽ
        .subscribe { println("$it on thread ${Thread.currentThread().name}") }
    Thread.sleep(1000)
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-context-03.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

�o�͂̈Ⴂ�͎��̂Ƃ���ł��B"RxComputationThreadPool" �ɒ��ڂ��Ă��������B

```text
1 on thread RxComputationThreadPool-1
2 on thread RxComputationThreadPool-1
3 on thread RxComputationThreadPool-1
```

<!--- TEST FLEXIBLE_THREAD -->

### ���ׂĂ𐧌䂷��R���[�`���R���e�L�X�g

�R���[�`���́A��ɉ��炩�̃R���e�L�X�g�œ��삵�Ă��܂��B ���Ƃ��΁A[runBlocking]���g�p���ă��C���X���b�h�ŃR���[�`�����J�n���ARx�o�[�W������ `rangeWithIntervalRx` ���Z�q�̌��ʂ�Rx `subscribe` ���Z�q���g�p����̂ł͂Ȃ������������܂��傤�B

<!--- INCLUDE
import io.reactivex.*
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.reactive.*
import io.reactivex.functions.BiFunction
import io.reactivex.schedulers.Schedulers
import java.util.concurrent.TimeUnit
-->

```kotlin
fun rangeWithIntervalRx(scheduler: Scheduler, time: Long, start: Int, count: Int): Flowable<Int> =
    Flowable.zip(
        Flowable.range(start, count),
        Flowable.interval(time, TimeUnit.MILLISECONDS, scheduler),
        BiFunction { x, _ -> x })

fun main(args: Array<String>) = runBlocking<Unit> {
    rangeWithIntervalRx(Schedulers.computation(), 100, 1, 3)
        .consumeEach { println("$it on thread ${Thread.currentThread().name}") }
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-context-04.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

���ʂƂ��ē����郁�b�Z�[�W�̓��C���X���b�h�Ńv�����g����܂��B

```text
1 on thread main
2 on thread main
3 on thread main
```

<!--- TEST LINES_START -->

### Unconfined�R���e�L�X�g

Most Rx operators do not have any specific thread (scheduler) associated with them and are working 
in whatever thread that they happen to be invoked in. We've seen it on the example of `subscribe` operator 
in the [threads with Rx](#threads-with-rx) section.
 
In the world of coroutines, [Unconfined] context serves a similar role. Let us modify our previous example,
but instead of iterating over the source `Flowable` from the `runBlocking` coroutine that is confined 
to the main thread, we launch a new coroutine in `Unconfined` context, while the main coroutine
simply waits its completion using [Job.join]:


�قƂ�ǂ�Rx���Z�q�͓���̃X���b�h�i�X�P�W���[���[�j�Ɋ֘A�t�����Ă��炸�A�Ăяo���ꂽ�X���b�h�œ��삵�܂��B
[Rx�̃X���b�h](#Rx�̃X���b�h)�Z�N�V������ `subscribe` ���Z�q�̗�Ō��Ă��܂����B

�R���[�`���̐��E�ł́A[Unconfined]�R���e�L�X�g�����l�̖������ʂ����܂��B
�O�̗��ύX���Ă݂܂��傤�B���C���X���b�h�Ɍ��肳�ꂽ `runBlocking` �R���[�`������\�[�X `Flowable` �𔽕�����̂ł͂Ȃ��A `Unconfined` �R���e�L�X�g�ŐV�����R���[�`�����N�����܂��B���C���R���[�`����[Job.join]���g�p���Ă���������҂����ł��B


<!--- INCLUDE
import io.reactivex.*
import kotlinx.coroutines.experimental.*
import kotlinx.coroutines.experimental.reactive.*
import io.reactivex.functions.BiFunction
import io.reactivex.schedulers.Schedulers
import java.util.concurrent.TimeUnit
-->

```kotlin
fun rangeWithIntervalRx(scheduler: Scheduler, time: Long, start: Int, count: Int): Flowable<Int> =
    Flowable.zip(
        Flowable.range(start, count),
        Flowable.interval(time, TimeUnit.MILLISECONDS, scheduler),
        BiFunction { x, _ -> x })

fun main(args: Array<String>) = runBlocking<Unit> {
    val job = launch(Unconfined) { // Unconfined�R���e�L�X�g�ŐV�����R���[�`�����N������i�Ǝ��̃X���b�h�v�[���Ȃ��j
        rangeWithIntervalRx(Schedulers.computation(), 100, 1, 3)
            .consumeEach { println("$it on thread ${Thread.currentThread().name}") }
    }
    job.join() // �R���[�`������������̂�҂�
}
```

> [����](kotlinx-coroutines-rx2/src/test/kotlin/guide/example-reactive-context-05.kt)�Ŋ��S�ȃR�[�h���擾�ł��܂�

�����ŏo�͂́ARx `subscribe` ���Z�q���g�p���������̗�̂悤�ɁA�R���[�`���̃R�[�h��Rx�v�Z�X���b�h�v�[���Ŏ��s����Ă��邱�Ƃ������Ă��܂��B

```text
1 on thread RxComputationThreadPool-1
2 on thread RxComputationThreadPool-1
3 on thread RxComputationThreadPool-1
```

<!--- TEST LINES_START -->

[Unconfined]�R���e�L�X�g�͒��ӂ��Ďg�p����ׂ��ł��B
����̃X�^�b�N���[�J���e�B���̌���ƃX�P�W���[�����O�̃I�[�o�[�w�b�h�̂��߂ɁA����̃e�X�g�̑S�̓I�ȃp�t�H�[�}���X�����シ��ꍇ������܂����A�X�^�b�N���[���Ȃ�A�g�p���Ă���R�[�h�̔񓯊����𐄑�����̂�����Ȃ�܂��B

�R���[�`�����`���l���ɗv�f�𑗂�ƁA[send][SendChannel.send]���Ăяo�����X���b�h��[Unconfined]�f�B�X�p�b�`���[�ŃR���[�`���̃R�[�h�̎��s���J�n���邱�Ƃ�����܂��B
`send` ���Ăяo�����̃v���f���[�T�R���[�`���́Aunconfined�̃R���V���[�}�[�R���[�`�������̒��f�|�C���g�ɒB����܂ňꎞ��~����܂��B
����́A�X���b�h�V�t�g���Z�q���Ȃ��ꍇ��Rx���E�ł̃��b�N�X�e�b�v�̃V���O���X���b�h�� `onNext` �̎��s�Ɣ��ɂ悭���Ă��܂��B
�I�y���[�^�͒ʏ�A���ɏ����ȃ`�����N�ō�Ƃ����Ă���A���G�ȏ����̂��߂ɑ����̉��Z�q����������K�v�����邽�߁ARx�̒ʏ�̃f�t�H���g�ł��B
�������A�R���[�`���ł͂��ꂪ�ُ�ł��B�R���[�`���ł́A�C�ӂ̕��G�ȏ������s�����Ƃ��ł��܂��B
�ʏ�A�����̃��[�J�[�R���[�`���ԂŃt�@���C���ƃt�@���A�E�g�������G�ȃp�C�v���C���̃X�g���[�������R���[�`�����`�F�[�����邾���ōς݂܂��B

<!--- MODULE kotlinx-coroutines-core -->
<!--- INDEX kotlinx.coroutines.experimental -->
[runBlocking]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/run-blocking.html
[Unconfined]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-unconfined/index.html
[yield]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/yield.html
[launch]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/launch.html
[CoroutineScope.context]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-coroutine-scope/context.html
[CommonPool]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-common-pool/index.html
[Job.join]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental/-job/join.html
<!--- INDEX kotlinx.coroutines.experimental.channels -->
[Channel]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-channel/index.html
[ReceiveChannel.receive]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-receive-channel/receive.html
[produce]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/produce.html
[consumeEach]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/consume-each.html
[ReceiveChannel]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-receive-channel/index.html
[SubscriptionReceiveChannel.close]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-subscription-receive-channel/close.html
[SendChannel.send]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-send-channel/send.html
[BroadcastChannel]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-broadcast-channel/index.html
[ConflatedBroadcastChannel]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-conflated-broadcast-channel/index.html
[ArrayBroadcastChannel]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.channels/-array-broadcast-channel/index.html
<!--- INDEX kotlinx.coroutines.experimental.selects -->
[select]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.selects/select.html
[whileSelect]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.experimental.selects/while-select.html
<!--- MODULE kotlinx-coroutines-reactive -->
<!--- INDEX kotlinx.coroutines.experimental.reactive -->
[publish]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-reactive/kotlinx.coroutines.experimental.reactive/publish.html
[org.reactivestreams.Publisher.consumeEach]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-reactive/kotlinx.coroutines.experimental.reactive/org.reactivestreams.-publisher/consume-each.html
[org.reactivestreams.Publisher.open]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-reactive/kotlinx.coroutines.experimental.reactive/org.reactivestreams.-publisher/open.html
<!--- MODULE kotlinx-coroutines-rx2 -->
<!--- INDEX kotlinx.coroutines.experimental.rx2 -->
[rxFlowable]: https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-rx2/kotlinx.coroutines.experimental.rx2/rx-flowable.html
<!--- END -->


