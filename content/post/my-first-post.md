---
title: "Agile code"
date: 2018-01-17T12:38:29+02:00
draft: false
tags: [agile]
draft: false
image: img/todo.jpg
---

# Lorem ipsum dolor sit amet

Nullam vel pellentesque ex. Morbi sed suscipit libero. Fusce iaculis ultrices libero, in interdum eros sodales ut. In sed mauris eu eros placerat tristique. Curabitur et ultricies velit, in lacinia lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Proin commodo sapien lacinia hendrerit gravida. Ut eleifend eleifend dui, sed hendrerit purus consectetur et. Ut mauris elit, maximus vitae massa eget, euismod malesuada mi. Phasellus ultricies metus nec nunc auctor finibus. In eu orci id dui porttitor lacinia in hendrerit est.

> Markdown is a lightweight markup language, originally created by John Gruber and Aaron Swartz allowing people "to write using an easy-to-read, easy-to-write plain text format, then convert it to structurally valid XHTML (or HTML)".

## Pellentesque habitant morbi

Nullam placerat, purus semper pharetra condimentum, enim neque feugiat elit, sed pellentesque ante enim quis nisi. Aenean leo diam, vestibulum vitae leo a, posuere laoreet nisi. Cras sodales nibh et magna aliquet condimentum. Cras massa metus, congue ac blandit sit amet, auctor at turpis. Ut accumsan lacus ut purus __consequat__, vel commodo urna tincidunt. Suspendisse potenti. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. In hac habitasse platea dictumst. Sed sit amet arcu et dui iaculis luctus. Aenean non pharetra nunc.

In cursus lobortis metus at luctus. Donec eu commodo dui. Nulla at diam id neque molestie feugiat. Donec diam ex, dapibus non malesuada a, iaculis ut **urna**. Phasellus pretium sed lectus at consequat. **Curabitur rhoncus** nibh ut orci vehicula, sit amet vulputate nisl sollicitudin. Nam eu massa sed tortor dignissim pulvinar. Etiam porta ac ex euismod auctor. Praesent egestas elementum venenatis.

    import java.util.LinkedList;
    import java.lang.reflect.Array;

    public class UnsortedHashSet<E> {

        private static final double LOAD_FACTOR_LIMIT = 0.7;

        private int size;
        private LinkedList<E>[] con;

        public UnsortedHashSet() {
            con  = (LinkedList<E>[])(new LinkedList[10]);
        }

        public boolean add(E obj) {
            int oldSize = size;
            int index = Math.abs(obj.hashCode()) % con.length;
            if(con[index] == null)
                con[index] = new LinkedList<E>();
            if(!con[index].contains(obj)) {
                con[index].add(obj);
                size++;

            }
            if(1.0 * size / con.length > LOAD_FACTOR_LIMIT)
                resize();
            return oldSize != size;
        }

        private void resize() {
            UnsortedHashSet<E> temp = new UnsortedHashSet<E>();
            temp.con = (LinkedList<E>[])(new LinkedList[con.length * 2 + 1]);
            for(int i = 0; i < con.length; i++){
                if(con[i] != null)
                    for(E e : con[i])
                        temp.add(e);
            }
            con = temp.con;
        }

        public int size() {
            return size;
        }
      }

In pulvinar cursus dolor id consequat. Phasellus pellentesque felis eget fringilla finibus. Curabitur molestie molestie tempus. Maecenas a ultricies massa, vestibulum venenatis sem. Donec iaculis aliquam lacus a blandit. Duis dapibus malesuada mauris ac interdum. Vivamus semper fringilla mauris in convallis. Sed porta erat vitae velit semper, vitae tincidunt mauris laoreet. Etiam eget luctus enim. Nullam vel congue lorem. Cras sagittis vel sem vitae cursus. Integer luctus auctor laoreet.

Phasellus efficitur est arcu, sed accumsan ipsum cursus at. Nam porta lectus ut hendrerit iaculis. Nam lacinia iaculis feugiat. Nam ultricies lobortis efficitur. Pellentesque blandit justo turpis, *in gravida nunc rhoncus nec*. Phasellus et nibh id urna lobortis eleifend vel in mi. Pellentesque vel nibh eleifend risus luctus scelerisque non ac nisi. Nulla consectetur tincidunt risus, ac tempor tortor convallis eu.

Donec imperdiet egestas auctor. Sed luctus arcu erat, **id suscipit velit congue a**. Duis non blandit nulla, a condimentum tellus. Nam ut metus est. Suspendisse potenti. Praesent sed quam lobortis, sodales diam eu, ultricies lectus. Sed finibus, erat non cursus consectetur, ex nulla fermentum lorem, id sollicitudin orci lectus at risus. Nunc vel tincidunt libero. Sed posuere vulputate ante, sit amet consectetur enim pulvinar sit amet.
