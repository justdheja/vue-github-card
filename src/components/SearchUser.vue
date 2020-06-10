<template>
  <form class="form">
    <input type="email" class="form__field" placeholder="Github Username" />
    <button type="button" class="btn btn--primary btn--inside uppercase">Search</button>
  </form>
</template>

<style lang="scss" scoped>
$background: #f5f6fa;
$text: #9c9c9c;
$input-bg-color: #fff;
$input-text-color: #a3a3a3;
$button-bg-color: #2c2d30;
$button-bg-color-mobile: #094256;
$button-text-color: #fff;

//** root
:root {
	background: $background;
	color: $text;
	font: 1rem "PT Sans", sans-serif;
}
a {
	color: inherit;
	
	&:hover {
		color: $button-bg-color;
	}
}

//** helper
.container {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}

.uppercase {
	text-transform: uppercase;
}

//** button
.btn {
  border-radius: 50%;
	display: inline-block;
	background: transparent;
	color: inherit;
	font: inherit;
	border: 0;
	outline: 0;
	padding: 0;
	transition: all 200ms ease-in;
	cursor: pointer;
	
	&--primary {
		background: $button-bg-color;
		color: $button-text-color;
		box-shadow: 0 0 10px 2px rgba(0, 0, 0, .1);
		border-radius: 5px;
		padding: 12px 36px;
		
		&:hover {
			background: darken($button-bg-color, 4%);
		}
		
		&:active {
			background: $button-bg-color;
			box-shadow: inset 0 0 10px 2px rgba(0, 0, 0, .2);
		}
	}
	
	&--inside {
		margin-left: -96px;
	}
}

//** form
.form {	
	&__field {
		width: 360px;
		background: #fff;
		color: $input-text-color;
		font: inherit;
		box-shadow: 0 6px 10px 0 rgba(0, 0, 0 , .1);
    border: 0;
    border-radius: 5px;
		outline: 0;
		padding: 22px 18px;
	}
}

// mobile

@media screen and (max-width: 1025px) {
  .form{
    &__field{
      width: 250px;
    }
  }
  .btn{
    &--primary{
      background: $button-bg-color-mobile;
    }
  }
}
</style>