# 이번주 리뷰

Django Signals

django 프레임워크는 특정 이벤트에서 신호(signal)를 발생시키는 기능을 가지고 있습니다.
이러한 신호는 함수 등을 실행시키는 트리거로 활용할 수 있습니다.

신호의 종류

1. django.db.models.signals.pre_save & django.db.models.signals.post_save:
   model에서 save() 전 또는 후에 알림
2. django.db.models.signals.pre_delete & django.db.models.signals.post_delete:
   model에서 delete() 전 또는 후에 알림
3. django.db.models.signals.m2m_changed:
   model에서 ManyToManyField가 변할 때 알림
4. django.core.signals.request_started & django.core.signals.request_finished:
   HTTP request가 시작 또는 완료에 알림
5. custom signals

사용
from django.db.models.signals import pre_save, post_save, pre_delete, post_delete, m2m_changed
from django.core.signals import request_started, request_finished
from django.dispatch import receiver

@receiver(pre_save, sender=모델명)
def 함수명(sender, instance, \*\*kwargs):
if instance.id is None:
pass
else:
current = instance
previous = 모델명.object.get(id=instance.id)
if previous.author != current.author:
pass

중요한 점
post_save()는 model에서 save()가 완료된 직후에 호출되는데,
post_save() 안에서 instance를 변경하기 위해 save()를 호출하면 무한 재귀에 빠지게 됩니다.
save() > post_save() > save() > post_save() > save() > ...
이런 경우 pre_save를 사용하여 해결하도록 합니다.

작동 순서(pre_save, post_save 예시)

1. model에서 save()를 호출
2. pre_save() 실행
3. save() 실행
4. post_save() 실행

참고:
https://docs.djangoproject.com/en/3.1/topics/signals/

# 튜터에게 궁금한 점
