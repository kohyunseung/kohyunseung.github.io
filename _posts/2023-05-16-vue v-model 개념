---
layout: archive
title: "Vue.js v-model"
---


# 자식 컴포넌트에서 부모의 data 내려 받아 변경하기

## props
부모 컴포넌트에서 자식 컴포넌트로 데이터를 내려주는 방법으로 props가 있습니다.

하지만 자식 컴포넌트에서는 부모 컴포넌트의 값을 변경 할 수 없습니다.

![](/assets/images/2023-05-16/1.png)

하지만 computed의 속성을 이용하여 ~~변경하는 것 처럼 보이게~~ 할 수 있습니다.

## computed

```vue
ParentComponent
<template>
	<ChildComponent :value="value" @update:value="val => (value = val)" />
</template>



ChildComponent
<template>
	<div>
		<input v-model="value" type="text" />
	</div>
</template>

<script>
export default {
	name: 'ChildComponent',
	computed: {
		value: {
			get() {
				return this.$attrs.value;
			},
			set(val) {
				this.$emit('update:value', val);
			},
		},
	},
};
</script>
```

computed의 get, set을 이용하여 emit으로 부모에서 변경하게 만드는 작업을 할 수 있습니다.

## v-model

이 속성을 이용하여 v-model을 이용하여 좀더 편리하게 사용 할 수 있습니다.

v-model은 위의 이벤트들의 축약형이라고 보시면 됩니다.
```vue
ParentComponent
<ChildComponent v-model="value" />


ChildComponent
<template>
	<div>
		<input v-model="value" type="text" />
	</div>
</template>

<script>
export default {
	name: 'ChildComponent',
	computed: {
		value: {
			get() {
				return this.$attrs.value;
			},
			set(val) {
				this.$emit('input', val);
			},
		},
	},
};
</script>
```

자 이제 값을 내려받아 변경 할 수 있는 구조가 되었습니다.

하지만 컴포넌트가 하나만 있는 것이 아니고 여러개가 있을때 일일히 작성하는 것은 매우 비효율적입니다.

## mixin

mixin을 이용하여 공통으로 사용 할 수 있게 만들어줍니다.

```vue
src/mixins/model.js
export default {
	computed: {
		model: {
			get() {
				return this.$attrs.value;
			},
			set(val) {
				this.$emit('input', val);
			},
		},
	},
};

ChildComponent
<template>
	<div>
		<input v-model="model" type="text" />
	</div>
</template>

<script>
import model from '@/mixins/model';
export default {
	name: 'ChildComponent',
	mixins: [model],
};
</script>
```

이렇게 mixin으로 공통으로 사용 할 수 있게 만든 후 변경이 필요한 컴포넌트에서 mixin을 import하여 사용 할 수 있습니다.